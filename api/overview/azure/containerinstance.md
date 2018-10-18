---
title: 適用於 .NET 的 Azure 容器執行個體程式庫
description: 適用於 .NET 的 Azure 容器執行個體程式庫參考
ms.date: 06/11/2018
ms.topic: reference
ms.service: container-instances
ms.openlocfilehash: 8642fc654546edde81aeaa520f52b2aff9720e55
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348100"
---
# <a name="azure-container-instances-libraries-for-net"></a>適用於 .NET 的 Azure 容器執行個體程式庫

使用適用於 .NET 的 Microsoft Azure 容器執行個體程式庫，來建立和管理 Azure 容器執行個體。 如需詳細資訊，請參閱 [Azure 容器執行個體概觀](/azure/container-instances/container-instances-overview)。

## <a name="management-library"></a>管理程式庫

使用管理程式庫來建立和管理 Azure 中的 Azure 容器執行個體。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a>範例來源

如果您想要查看下列程式碼範例在相關情境中的應用，您可以在下列 GitHub 存放庫中找到這些範例：

[Azure-Samples/aci-docs-sample-dotnet](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a>驗證

驗證 SDK 用戶端其中一個最輕鬆的方法，就是使用[檔案型驗證][sdk-auth]。 檔案型驗證會在具現化 [IAzure][iazure] 用戶端物件時部析認證檔案，並接著在進行 Azure 驗證時使用這些認證。 若要使用檔案式驗證：

1. 使用 [Azure CLI](/cli/azure) 或 [Cloud Shell](https://shell.azure.com/) 建立認證檔案：

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   如果您使用 [Cloud Shell](https://shell.azure.com/) 產生認證檔案，請將其內容複製到 .NET 應用程式可以存取的本機檔案中。

2. 將 `AZURE_AUTH_LOCATION` 環境變數設定為所產生認證檔案的完整路徑。 例如 (在 Bash 殼層中)：

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

一旦您建立了認證檔案並植入了 `AZURE_AUTH_LOCATION` 環境變數，請使用 [Azure.Authenticate][iazure-authenticate] 方法來初始化 [IAzure][iazure] 用戶端物件。 範例專案首先會獲得 `AZURE_AUTH_LOCATION` 值，接著呼叫傳回初始化 `IAzure` 用戶端物件的方法：

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]

此方法來自範例應用程式傳回初始化的 [IAzure][iazure] 執行個體，並接著將其做為第一個參數傳遞給範例中所有其他方法：

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]

若要深入了解 Azure 的 .NET 管理程式庫中有哪些可用驗證方法，請參閱[使用適用於 .NET 的 Azure 管理程式庫來進行驗證][sdk-auth]。

## <a name="create-container-group---single-container"></a>建立容器群組 - 單一容器

此範例會建立一個容器群組搭配單一容器。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>建立容器群組 - 多個容器

此範例會建立一個容器群組搭配兩個容器：分別是應用程式容器和側車容器。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

## <a name="asynchronous-container-create-with-polling"></a>使用輪詢建立非同步容器

此範例會使用非同步建立方式，來建立一個容器群組搭配單一容器。 接著，會輪詢 Azure 容器群組，再輸出容器群組的狀態，直到狀態顯示為「執行中」為止。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

## <a name="create-task-based-container-group"></a>立工作型容器群組

此範例會建立一個容器群組搭配單一工作型容器。 該容器會以「絕不」[重新啟動原則](/azure/container-instances/container-instances-restart-policy)和[自訂命令列](/azure/container-instances/container-instances-restart-policy#command-line-override)來設定。

如果您想要使用數個命令列引數執行單一命令，例如 `echo FOO BAR`，則必須以字串陣列方式提供給 `WithStartingCommandLines` 方法。 例如︰

`WithStartingCommandLines("echo", "FOO", "BAR")`

然而，如果您想要(或可能會) 使用多個引數來執行多個命令，則必須執行殼層，並將鏈結的命令做為引數傳遞。 例如，這樣會執行 `echo` 和 `tail` 命令：

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

## <a name="list-container-groups"></a>列出容器群組

此範例會列出資源群組中的容器群組。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

## <a name="get-an-existing-container-group"></a>取得現有的容器群組

此範例會取得位於資源群組中的特定容器群組，且會列印出這些容器群組的屬性和值。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

## <a name="delete-a-container-group"></a>刪除容器群組

此範例會從資源群組中刪除容器群組。

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a>API 參考資料

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a>範例

* 您可以在 GitHub 中找到先前範例的原始程式碼：

  [Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]

* 更多 Azure 容器執行個體程式碼範例：

  [Azure 程式碼範例][samples]

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
