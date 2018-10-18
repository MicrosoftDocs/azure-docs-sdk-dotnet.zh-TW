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
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="99532-103">適用於 .NET 的 Azure 容器執行個體程式庫</span><span class="sxs-lookup"><span data-stu-id="99532-103">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="99532-104">使用適用於 .NET 的 Microsoft Azure 容器執行個體程式庫，來建立和管理 Azure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="99532-104">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="99532-105">如需詳細資訊，請參閱 [Azure 容器執行個體概觀](/azure/container-instances/container-instances-overview)。</span><span class="sxs-lookup"><span data-stu-id="99532-105">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="99532-106">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="99532-106">Management library</span></span>

<span data-ttu-id="99532-107">使用管理程式庫來建立和管理 Azure 中的 Azure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="99532-107">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="99532-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="99532-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="99532-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="99532-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a><span data-ttu-id="99532-110">範例來源</span><span class="sxs-lookup"><span data-stu-id="99532-110">Example source</span></span>

<span data-ttu-id="99532-111">如果您想要查看下列程式碼範例在相關情境中的應用，您可以在下列 GitHub 存放庫中找到這些範例：</span><span class="sxs-lookup"><span data-stu-id="99532-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="99532-112">Azure-Samples/aci-docs-sample-dotnet</span><span class="sxs-lookup"><span data-stu-id="99532-112">Azure-Samples/aci-docs-sample-dotnet</span></span>](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a><span data-ttu-id="99532-113">驗證</span><span class="sxs-lookup"><span data-stu-id="99532-113">Authentication</span></span>

<span data-ttu-id="99532-114">驗證 SDK 用戶端其中一個最輕鬆的方法，就是使用[檔案型驗證][sdk-auth]。</span><span class="sxs-lookup"><span data-stu-id="99532-114">One of the easiest ways to authenticate SDK clients is with [file-based authentication][sdk-auth].</span></span> <span data-ttu-id="99532-115">檔案型驗證會在具現化 [IAzure][iazure] 用戶端物件時部析認證檔案，並接著在進行 Azure 驗證時使用這些認證。</span><span class="sxs-lookup"><span data-stu-id="99532-115">File-based authentication parses a credentials file when instantiating the [IAzure][iazure] client object, which then uses those credentials when authenticating with Azure.</span></span> <span data-ttu-id="99532-116">若要使用檔案式驗證：</span><span class="sxs-lookup"><span data-stu-id="99532-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="99532-117">使用 [Azure CLI](/cli/azure) 或 [Cloud Shell](https://shell.azure.com/) 建立認證檔案：</span><span class="sxs-lookup"><span data-stu-id="99532-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="99532-118">如果您使用 [Cloud Shell](https://shell.azure.com/) 產生認證檔案，請將其內容複製到 .NET 應用程式可以存取的本機檔案中。</span><span class="sxs-lookup"><span data-stu-id="99532-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your .NET application can access.</span></span>

2. <span data-ttu-id="99532-119">將 `AZURE_AUTH_LOCATION` 環境變數設定為所產生認證檔案的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="99532-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="99532-120">例如 (在 Bash 殼層中)：</span><span class="sxs-lookup"><span data-stu-id="99532-120">For example (in the Bash shell):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="99532-121">一旦您建立了認證檔案並植入了 `AZURE_AUTH_LOCATION` 環境變數，請使用 [Azure.Authenticate][iazure-authenticate] 方法來初始化 [IAzure][iazure] 用戶端物件。</span><span class="sxs-lookup"><span data-stu-id="99532-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the [Azure.Authenticate][iazure-authenticate] method to initialize the [IAzure][iazure] client object.</span></span> <span data-ttu-id="99532-122">範例專案首先會獲得 `AZURE_AUTH_LOCATION` 值，接著呼叫傳回初始化 `IAzure` 用戶端物件的方法：</span><span class="sxs-lookup"><span data-stu-id="99532-122">The example project first obtains the `AZURE_AUTH_LOCATION` value, then calls a method that returns an initialized `IAzure` client object:</span></span>

<span data-ttu-id="99532-123"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span><span class="sxs-lookup"><span data-stu-id="99532-123"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]</span></span>

<span data-ttu-id="99532-124">此方法來自範例應用程式傳回初始化的 [IAzure][iazure] 執行個體，並接著將其做為第一個參數傳遞給範例中所有其他方法：</span><span class="sxs-lookup"><span data-stu-id="99532-124">This method from the sample application returns the initialized [IAzure][iazure] instance, which is then passed as the first parameter to all other methods in the sample:</span></span>

<span data-ttu-id="99532-125"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span><span class="sxs-lookup"><span data-stu-id="99532-125"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]</span></span>

<span data-ttu-id="99532-126">若要深入了解 Azure 的 .NET 管理程式庫中有哪些可用驗證方法，請參閱[使用適用於 .NET 的 Azure 管理程式庫來進行驗證][sdk-auth]。</span><span class="sxs-lookup"><span data-stu-id="99532-126">For more details about the available authentication methods in the .NET management libraries for Azure, see [Authentication in Azure Management Libraries for .NET][sdk-auth].</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="99532-127">建立容器群組 - 單一容器</span><span class="sxs-lookup"><span data-stu-id="99532-127">Create container group - single container</span></span>

<span data-ttu-id="99532-128">此範例會建立一個容器群組搭配單一容器。</span><span class="sxs-lookup"><span data-stu-id="99532-128">This example creates a container group with a single container.</span></span>

<span data-ttu-id="99532-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span><span class="sxs-lookup"><span data-stu-id="99532-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]</span></span>

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="99532-130">建立容器群組 - 多個容器</span><span class="sxs-lookup"><span data-stu-id="99532-130">Create container group - multiple containers</span></span>

<span data-ttu-id="99532-131">此範例會建立一個容器群組搭配兩個容器：分別是應用程式容器和側車容器。</span><span class="sxs-lookup"><span data-stu-id="99532-131">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<span data-ttu-id="99532-132"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span><span class="sxs-lookup"><span data-stu-id="99532-132"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]</span></span>

## <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="99532-133">使用輪詢建立非同步容器</span><span class="sxs-lookup"><span data-stu-id="99532-133">Asynchronous container create with polling</span></span>

<span data-ttu-id="99532-134">此範例會使用非同步建立方式，來建立一個容器群組搭配單一容器。</span><span class="sxs-lookup"><span data-stu-id="99532-134">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="99532-135">接著，會輪詢 Azure 容器群組，再輸出容器群組的狀態，直到狀態顯示為「執行中」為止。</span><span class="sxs-lookup"><span data-stu-id="99532-135">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<span data-ttu-id="99532-136"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span><span class="sxs-lookup"><span data-stu-id="99532-136"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]</span></span>

## <a name="create-task-based-container-group"></a><span data-ttu-id="99532-137">立工作型容器群組</span><span class="sxs-lookup"><span data-stu-id="99532-137">Create task-based container group</span></span>

<span data-ttu-id="99532-138">此範例會建立一個容器群組搭配單一工作型容器。</span><span class="sxs-lookup"><span data-stu-id="99532-138">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="99532-139">該容器會以「絕不」[重新啟動原則](/azure/container-instances/container-instances-restart-policy)和[自訂命令列](/azure/container-instances/container-instances-restart-policy#command-line-override)來設定。</span><span class="sxs-lookup"><span data-stu-id="99532-139">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="99532-140">如果您想要使用數個命令列引數執行單一命令，例如 `echo FOO BAR`，則必須以字串陣列方式提供給 `WithStartingCommandLines` 方法。</span><span class="sxs-lookup"><span data-stu-id="99532-140">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="99532-141">例如︰</span><span class="sxs-lookup"><span data-stu-id="99532-141">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="99532-142">然而，如果您想要(或可能會) 使用多個引數來執行多個命令，則必須執行殼層，並將鏈結的命令做為引數傳遞。</span><span class="sxs-lookup"><span data-stu-id="99532-142">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="99532-143">例如，這樣會執行 `echo` 和 `tail` 命令：</span><span class="sxs-lookup"><span data-stu-id="99532-143">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<span data-ttu-id="99532-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span><span class="sxs-lookup"><span data-stu-id="99532-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]</span></span>

## <a name="list-container-groups"></a><span data-ttu-id="99532-145">列出容器群組</span><span class="sxs-lookup"><span data-stu-id="99532-145">List container groups</span></span>

<span data-ttu-id="99532-146">此範例會列出資源群組中的容器群組。</span><span class="sxs-lookup"><span data-stu-id="99532-146">This example lists the container groups in a resource group.</span></span>

<span data-ttu-id="99532-147"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span><span class="sxs-lookup"><span data-stu-id="99532-147"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]</span></span>

## <a name="get-an-existing-container-group"></a><span data-ttu-id="99532-148">取得現有的容器群組</span><span class="sxs-lookup"><span data-stu-id="99532-148">Get an existing container group</span></span>

<span data-ttu-id="99532-149">此範例會取得位於資源群組中的特定容器群組，且會列印出這些容器群組的屬性和值。</span><span class="sxs-lookup"><span data-stu-id="99532-149">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<span data-ttu-id="99532-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span><span class="sxs-lookup"><span data-stu-id="99532-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]</span></span>

## <a name="delete-a-container-group"></a><span data-ttu-id="99532-151">刪除容器群組</span><span class="sxs-lookup"><span data-stu-id="99532-151">Delete a container group</span></span>

<span data-ttu-id="99532-152">此範例會從資源群組中刪除容器群組。</span><span class="sxs-lookup"><span data-stu-id="99532-152">This example deletes a container group from a resource group.</span></span>

<span data-ttu-id="99532-153"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span><span class="sxs-lookup"><span data-stu-id="99532-153"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet --> [!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]</span></span>

## <a name="api-reference"></a><span data-ttu-id="99532-154">API 參考資料</span><span class="sxs-lookup"><span data-stu-id="99532-154">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="99532-155">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="99532-155">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="99532-156">範例</span><span class="sxs-lookup"><span data-stu-id="99532-156">Samples</span></span>

* <span data-ttu-id="99532-157">您可以在 GitHub 中找到先前範例的原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="99532-157">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="99532-158">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="99532-158">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="99532-159">更多 Azure 容器執行個體程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="99532-159">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="99532-160">[Azure 程式碼範例][samples]</span><span class="sxs-lookup"><span data-stu-id="99532-160">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="99532-161">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="99532-161">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
