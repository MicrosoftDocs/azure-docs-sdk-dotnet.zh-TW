---
title: 適用於 .NET 的 Azure Active Directory 程式庫
description: 適用於 .NET 的 Azure Active Directory 程式庫參考
keywords: Azure, .NET, SDK, API, AAD, Active Directory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: active-directory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: a5a228fcde29dbef6a6e8d0482121ee710b002a4
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065858"
---
# <a name="azure-active-directory-libraries-for-net"></a>適用於 .NET 的 Azure Active Directory 程式庫

## <a name="overview"></a>概觀

使用 Azure Active Directory 登入使用者並管理應用程式及 API 的存取。

若要開始使用 Azure Active Directory，請參閱[搭配 Azure AD 的 ASP.NET Web 應用程式登入和登出](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)。

## <a name="client-library"></a>用戶端程式庫

透過 OAuth2、 OpenID Connect、Active Directory 圖形 API 驗證或 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 來連線和驗證使用者或應用程式。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a>程式碼範例

擷取桌面應用程式的存取權杖。

```csharp
/* Include this "using" directive...
using Microsoft.IdentityModel.Clients.ActiveDirectory;
*/

AuthenticationResult result = null;
AuthenticationContext authContext = new AuthenticationContext("https://someauthority.com");
try
{
    result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
}
catch (AdalException ex)
{
    // An unexpected error occurred, or user canceled the sign in.
    if (ex.ErrorCode != "access_denied")
        MessageBox.Show(ex.Message);

    return;
}
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a>範例

* [使用 OpenID Connect 驗證來自 Azure AD 租用戶的使用者](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [使用 Oauth2 以應用程式權限呼叫 Web API](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [在應用程式中使用角色型存取控制 (RBAC)](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

探索 [Azure Active Directory 程式碼範例](/azure/active-directory/develop/active-directory-code-samples)的完整集合。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
