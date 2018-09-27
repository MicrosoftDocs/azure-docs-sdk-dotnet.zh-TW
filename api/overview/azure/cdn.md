---
title: 適用於 .NET 的 Azure CDN 程式庫
description: 適用於 .NET 的 Azure CDN 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: cdn
ms.openlocfilehash: 6475edbe4fa0d01739de5cff76038aa6e7fd2cf9
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190121"
---
# <a name="azure-cdn-libraries-for-net"></a>適用於 .NET 的 Azure CDN 程式庫

## <a name="overview"></a>概觀

Azure 內容傳遞網路 (CDN) 會在策略性放置的位置上快取靜態 Web 內容，以提供最大輸送量來將內容傳遞給使用者。 CDN 為開發人員提供一套全球解決方案，以在全球實體節點上快取內容來傳遞高頻寬內容。

若要深入了解 Azure CDN，請參閱 [Azure 內容傳遞網路的概觀](https://docs.microsoft.com/azure/cdn/cdn-overview)。


## <a name="management-library"></a>管理程式庫

您可以使用適用於 .NET 的 Azure CDN 程式庫，自動建立和管理 CDN 設定檔與端點。 

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a>範例

此範例會使用指向 `www.contoso.com` 的新端點來建立新的 CDN 設定檔。

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
> [探索管理 API](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a>範例

* [在 .NET 中開始使用 CDN - 管理 CDN](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
