---
title: "適用於 .NET 的 Azure Resource Manager 程式庫"
description: "適用於 .NET 的 Azure Resource Manager 程式庫參考"
keywords: Azure, .NET, SDK, API, Resource Manager
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f9fe96fcdc94d3d27445f462c5220def9f2966da
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="72bda-104">適用於 .NET 的 Azure Resource Manager 程式庫</span><span class="sxs-lookup"><span data-stu-id="72bda-104">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="72bda-105">概觀</span><span class="sxs-lookup"><span data-stu-id="72bda-105">Overview</span></span>

<span data-ttu-id="72bda-106">Azure Resource Manager 可讓您將方案中的資源作為群組使用。</span><span class="sxs-lookup"><span data-stu-id="72bda-106">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="72bda-107">如需 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview)。</span><span class="sxs-lookup"><span data-stu-id="72bda-107">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="72bda-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="72bda-108">Management library</span></span>

<span data-ttu-id="72bda-109">適用於 .NET 的 Azure Resource Manager 程式庫可讓您建立、更新、刪除及列出資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="72bda-109">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="72bda-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="72bda-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="72bda-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="72bda-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="72bda-112">範例</span><span class="sxs-lookup"><span data-stu-id="72bda-112">Example</span></span>

<span data-ttu-id="72bda-113">此範例會建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="72bda-113">This example creates a new resource group.</span></span>

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
> [<span data-ttu-id="72bda-114">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="72bda-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="72bda-115">範例</span><span class="sxs-lookup"><span data-stu-id="72bda-115">Samples</span></span>

* [<span data-ttu-id="72bda-116">管理資源群組</span><span class="sxs-lookup"><span data-stu-id="72bda-116">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="72bda-117">管理資源</span><span class="sxs-lookup"><span data-stu-id="72bda-117">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="72bda-118">使用 ARM 範本部署資源</span><span class="sxs-lookup"><span data-stu-id="72bda-118">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="72bda-119">使用 ARM 範本部署資源 (帶有進度)</span><span class="sxs-lookup"><span data-stu-id="72bda-119">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
