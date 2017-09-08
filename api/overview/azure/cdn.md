---
title: "適用於 .NET 的 Azure CDN 程式庫"
description: "適用於 .NET 的 Azure CDN 程式庫參考"
keywords: Azure, .NET, SDK, API, CDN
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cdn
ms.openlocfilehash: 1582f85c6e25a973fdf0294afb4393e6622e92a0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cdn-libraries-for-net"></a><span data-ttu-id="8215e-104">適用於 .NET 的 Azure CDN 程式庫</span><span class="sxs-lookup"><span data-stu-id="8215e-104">Azure CDN libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8215e-105">概觀</span><span class="sxs-lookup"><span data-stu-id="8215e-105">Overview</span></span>

<span data-ttu-id="8215e-106">Azure 內容傳遞網路 (CDN) 會在策略性放置的位置上快取靜態 Web 內容，以提供最大輸送量來將內容傳遞給使用者。</span><span class="sxs-lookup"><span data-stu-id="8215e-106">The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="8215e-107">CDN 為開發人員提供一套全球解決方案，以在全球實體節點上快取內容來傳遞高頻寬內容。</span><span class="sxs-lookup"><span data-stu-id="8215e-107">The CDN offers developers a global solution for delivering high-bandwidth content by caching the content at physical nodes across the world.</span></span>

<span data-ttu-id="8215e-108">若要深入了解 Azure CDN，請參閱 [Azure 內容傳遞網路的概觀](https://docs.microsoft.com/azure/cdn/cdn-overview)。</span><span class="sxs-lookup"><span data-stu-id="8215e-108">To learn more about Azure CDN, see [Overview of the Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn/cdn-overview).</span></span>


## <a name="management-library"></a><span data-ttu-id="8215e-109">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="8215e-109">Management library</span></span>

<span data-ttu-id="8215e-110">您可以使用適用於 .NET 的 Azure CDN 程式庫，自動建立和管理 CDN 設定檔與端點。</span><span class="sxs-lookup"><span data-stu-id="8215e-110">You can use the Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.</span></span> 

<span data-ttu-id="8215e-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="8215e-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8215e-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="8215e-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a><span data-ttu-id="8215e-113">範例</span><span class="sxs-lookup"><span data-stu-id="8215e-113">Example</span></span>

<span data-ttu-id="8215e-114">此範例會使用指向 `www.contoso.com` 的新端點來建立新的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="8215e-114">This example creates a new CDN profile with a new endpoint pointed to `www.contoso.com`.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8215e-115">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="8215e-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a><span data-ttu-id="8215e-116">範例</span><span class="sxs-lookup"><span data-stu-id="8215e-116">Samples</span></span>

* [<span data-ttu-id="8215e-117">在 .NET 中開始使用 CDN - 管理 CDN</span><span class="sxs-lookup"><span data-stu-id="8215e-117">Getting started with CDN - Manage CDN - in .NET</span></span>](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
