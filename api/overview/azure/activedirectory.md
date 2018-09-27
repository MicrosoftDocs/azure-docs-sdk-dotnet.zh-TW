---
title: 適用於 .NET 的 Azure Active Directory 程式庫
description: 適用於 .NET 的 Azure Active Directory 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: active-directory
ms.openlocfilehash: 0226f06546f7dc14b9ab3392008744754d47a19a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190221"
---
# <a name="azure-active-directory-libraries-for-net"></a><span data-ttu-id="6aaee-103">適用於 .NET 的 Azure Active Directory 程式庫</span><span class="sxs-lookup"><span data-stu-id="6aaee-103">Azure Active Directory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6aaee-104">概觀</span><span class="sxs-lookup"><span data-stu-id="6aaee-104">Overview</span></span>

<span data-ttu-id="6aaee-105">使用 Azure Active Directory 登入使用者並管理應用程式及 API 的存取。</span><span class="sxs-lookup"><span data-stu-id="6aaee-105">Sign-on users and manage access to applications and APIs with Azure Active Directory.</span></span>

<span data-ttu-id="6aaee-106">若要開始使用 Azure Active Directory，請參閱[搭配 Azure AD 的 ASP.NET Web 應用程式登入和登出](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="6aaee-106">To get started with Azure Active Directory, see [ASP.NET web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="6aaee-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="6aaee-107">Client library</span></span>

<span data-ttu-id="6aaee-108">透過 OAuth2、 OpenID Connect、Active Directory 圖形 API 驗證或 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) 來連線和驗證使用者或應用程式。</span><span class="sxs-lookup"><span data-stu-id="6aaee-108">Connect and authenticate users or applications over OAuth2, OpenID Connect, Active Directory Graph API authentication or [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span></span>

<span data-ttu-id="6aaee-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="6aaee-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6aaee-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="6aaee-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a><span data-ttu-id="6aaee-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="6aaee-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a><span data-ttu-id="6aaee-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6aaee-112">Code Example</span></span>

<span data-ttu-id="6aaee-113">擷取桌面應用程式的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="6aaee-113">Retrieve an access token for a desktop application.</span></span>

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
> [<span data-ttu-id="6aaee-114">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="6aaee-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a><span data-ttu-id="6aaee-115">範例</span><span class="sxs-lookup"><span data-stu-id="6aaee-115">Samples</span></span>

* [<span data-ttu-id="6aaee-116">使用 OpenID Connect 驗證來自 Azure AD 租用戶的使用者</span><span class="sxs-lookup"><span data-stu-id="6aaee-116">Use OpenID Connect to authenticate users from an Azure AD tenant</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [<span data-ttu-id="6aaee-117">使用 Oauth2 以應用程式權限呼叫 Web API</span><span class="sxs-lookup"><span data-stu-id="6aaee-117">Use Oauth2 to call a web API with application permissions</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [<span data-ttu-id="6aaee-118">在應用程式中使用角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="6aaee-118">Use role-based access control (RBAC) in an application</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

<span data-ttu-id="6aaee-119">探索 [Azure Active Directory 程式碼範例](/azure/active-directory/develop/active-directory-code-samples)的完整集合。</span><span class="sxs-lookup"><span data-stu-id="6aaee-119">Explore the full collection of [Azure Active Directory code samples](/azure/active-directory/develop/active-directory-code-samples).</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
