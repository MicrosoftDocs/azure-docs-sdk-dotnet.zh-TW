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
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="9cde3-103">適用於 .NET 的 Azure Resource Manager 程式庫</span><span class="sxs-lookup"><span data-stu-id="9cde3-103">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="9cde3-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9cde3-104">Overview</span></span>

<span data-ttu-id="9cde3-105">Azure Resource Manager 可讓您將方案中的資源作為群組使用。</span><span class="sxs-lookup"><span data-stu-id="9cde3-105">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="9cde3-106">如需 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。</span><span class="sxs-lookup"><span data-stu-id="9cde3-106">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="9cde3-107">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="9cde3-107">Management library</span></span>

<span data-ttu-id="9cde3-108">適用於 .NET 的 Azure Resource Manager 程式庫可讓您建立、更新、刪除及列出資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="9cde3-108">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="9cde3-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="9cde3-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9cde3-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9cde3-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="9cde3-111">範例</span><span class="sxs-lookup"><span data-stu-id="9cde3-111">Example</span></span>

<span data-ttu-id="9cde3-112">此範例會建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9cde3-112">This example creates a new resource group.</span></span>

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
> [<span data-ttu-id="9cde3-113">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="9cde3-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="9cde3-114">範例</span><span class="sxs-lookup"><span data-stu-id="9cde3-114">Samples</span></span>

* [<span data-ttu-id="9cde3-115">管理資源群組</span><span class="sxs-lookup"><span data-stu-id="9cde3-115">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="9cde3-116">管理資源</span><span class="sxs-lookup"><span data-stu-id="9cde3-116">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="9cde3-117">使用 ARM 範本部署資源</span><span class="sxs-lookup"><span data-stu-id="9cde3-117">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="9cde3-118">使用 ARM 範本部署資源 (帶有進度)</span><span class="sxs-lookup"><span data-stu-id="9cde3-118">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
