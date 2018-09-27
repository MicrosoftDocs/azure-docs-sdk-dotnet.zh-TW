---
title: 適用於 .NET 的 Azure Resource Manager 程式庫
description: 適用於 .NET 的 Azure Resource Manager 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 6d3a27c5f7ba94f5579723cc4f798826c8bdefd6
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190837"
---
# <a name="azure-resource-manager-libraries-for-net"></a>適用於 .NET 的 Azure Resource Manager 程式庫

## <a name="overview"></a>概觀

Azure Resource Manager 可讓您將方案中的資源作為群組使用。  如需 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。

## <a name="management-library"></a>管理程式庫

適用於 .NET 的 Azure Resource Manager 程式庫可讓您建立、更新、刪除及列出資源與資源群組。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a>範例

此範例會建立新的資源群組。

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a>範例

* [管理資源群組](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [管理資源](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [使用 ARM 範本部署資源](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [使用 ARM 範本部署資源 (帶有進度)](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
