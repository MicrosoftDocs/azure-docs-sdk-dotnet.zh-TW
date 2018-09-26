---
title: 保護 Azure 應用程式的 .NET 教學課程
description: 在 Azure 上執行之 .NET 應用程式的應用程式安全性和身分識別管理教學課程。
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 88ecfc69fbd57becf1adf1163a063c0d2bb086a8
ms.sourcegitcommit: 61638b504b6c4d96b357894835c80c2680a99fe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750586"
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a><span data-ttu-id="923b3-103">驗證在 Azure 上執行之 .NET 應用程式的使用者教學課程</span><span class="sxs-lookup"><span data-stu-id="923b3-103">Tutorials for authenticating users in your .NET apps running on Azure</span></span>

<span data-ttu-id="923b3-104">下表連結到驗證使用者和保護在 Azure 上執行之 .NET 應用程式的深入教學課程。</span><span class="sxs-lookup"><span data-stu-id="923b3-104">The following table links to in-depth tutorials for authenticating users and securing .NET applications running on Azure.</span></span>

<span data-ttu-id="923b3-105">如需範例原始程式碼，請參閱 [Azure 服務範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)清單。</span><span class="sxs-lookup"><span data-stu-id="923b3-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>

| | |
|---|---|
|<span data-ttu-id="923b3-106">**Active Directory**</span><span class="sxs-lookup"><span data-stu-id="923b3-106">**Active Directory**</span></span>||
| <span data-ttu-id="923b3-107">[使用 Visual Studio 連線服務將 Azure Active Directory 新增至 Web 應用程式][5]</span><span class="sxs-lookup"><span data-stu-id="923b3-107">[Add Azure Active Directory to your web application by using Visual Studio Connected Services][5]</span></span> | <span data-ttu-id="923b3-108">將 Web 應用程式連線至 Visual Studio 中的 Azure AD</span><span class="sxs-lookup"><span data-stu-id="923b3-108">Connect a web app to Azure AD in Visual Studio</span></span> |
| <span data-ttu-id="923b3-109">[搭配 Azure AD 的 Web 應用程式登入和登出][1]</span><span class="sxs-lookup"><span data-stu-id="923b3-109">[Web app sign-in and sign-out with Azure AD][1]</span></span> | <span data-ttu-id="923b3-110">使用 ADAL 程式庫將使用者登入和登出您的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="923b3-110">Sign users in and out of your ASP.NET with the ADAL library.</span></span> |
| <span data-ttu-id="923b3-111">[使用 Azure AD 進行桌面應用程式驗證][2]</span><span class="sxs-lookup"><span data-stu-id="923b3-111">[Desktop application authentication with Azure AD][2]</span></span>| <span data-ttu-id="923b3-112">使用 ADAL 將 Azure AD 整合至 Windows 桌面 WPF 應用程式。</span><span class="sxs-lookup"><span data-stu-id="923b3-112">Integrate Azure AD into a Windows Desktop WPF app using ADAL.</span></span> | 
| <span data-ttu-id="923b3-113">[使用 Azure AD 進行 Web API 驗證][3]</span><span class="sxs-lookup"><span data-stu-id="923b3-113">[Web API authentication with Azure AD][3]</span></span> | <span data-ttu-id="923b3-114">使用 Azure AD 的持有者權杖來保護 Web API。</span><span class="sxs-lookup"><span data-stu-id="923b3-114">Protect a web API using bearer tokens from Azure AD.</span></span> |
|<span data-ttu-id="923b3-115">**金鑰保存庫**</span><span class="sxs-lookup"><span data-stu-id="923b3-115">**Key Vault**</span></span>||
| <span data-ttu-id="923b3-116">[使用 Visual Studio 連線服務在 Web 應用程式中新增 Key Vault][6]</span><span class="sxs-lookup"><span data-stu-id="923b3-116">[Add Key Vault to your web application by using Visual Studio Connected Services][6]</span></span> | <span data-ttu-id="923b3-117">將 Web 應用程式連線至 Visual Studio 中的 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="923b3-117">Connect a web app to Azure Key Vault in Visual Studio</span></span> |
| <span data-ttu-id="923b3-118">[從 Web 應用程式使用 Azure Key Vault][4]</span><span class="sxs-lookup"><span data-stu-id="923b3-118">[Use Azure Key Vault from a Web Application][4]</span></span> | <span data-ttu-id="923b3-119">從 Azure Key Vault 存取祕密，以便在 Web 應用程式中使用該祕密。</span><span class="sxs-lookup"><span data-stu-id="923b3-119">Access a secret from an Azure Key Vault so that it can be used in your web application.</span></span> | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service