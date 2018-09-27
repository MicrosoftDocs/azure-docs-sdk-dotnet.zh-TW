---
title: 適用於 .NET 的 Azure App Service 程式庫
description: 適用於 .NET 的 Azure App Service 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: app-service
ms.openlocfilehash: 82f8eccfafd2f7b1cf1df1ce0f40212509ccddd3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189991"
---
# <a name="azure-app-service-libraries-for-net"></a>適用於 .NET 的 Azure App Service 程式庫

## <a name="overview"></a>概觀

[Azure App Service](/azure/app-service/app-service-value-prop-what-is) 可讓您部署及調整網站、Web 應用程式、服務和 REST API。

## <a name="management-api"></a>管理 API

使用管理 API 來部署、管理及調整裝載在 Azure App Service 中的元素。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。


#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a>程式碼範例

建立新的 Web 應用程式。

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.AppService.Fluent;
*/

IWebApp app1 = azure.WebApps
    .Define("MyUniqueWebAddress")
    .WithRegion(Region.USWest)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewWindowsPlan(PricingTier.StandardS1)
    .Create();
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a>範例

* [使用適用於 Azure 的 .NET SDK 來管理 Web 應用程式](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [Azure App Service 的 ASP.NET 範例](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

檢視 Azure App Service 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package