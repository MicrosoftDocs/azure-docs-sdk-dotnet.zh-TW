---
title: "保護 Azure 應用程式的 .NET 教學課程"
description: "在 Azure 上執行之 .NET 應用程式的應用程式安全性和身分識別管理教學課程。"
author: camsoper
manager: douge
ms.devlang: dotnet
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 06/09/2017
ms.author: casoper
ms.openlocfilehash: 1ac3b8168f8c2b11082536b635fc32b607354711
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a><span data-ttu-id="98152-103">驗證在 Azure 上執行之 .NET 應用程式的使用者教學課程</span><span class="sxs-lookup"><span data-stu-id="98152-103">Tutorials for authenticating users in your .NET apps running on Azure</span></span>

<span data-ttu-id="98152-104">下表連結到驗證使用者和保護在 Azure 上執行之 .NET 應用程式的深入教學課程。</span><span class="sxs-lookup"><span data-stu-id="98152-104">The following table links to in-depth tutorials for authenticating users and securing .NET applications running on Azure.</span></span>

<span data-ttu-id="98152-105">如需範例原始程式碼，請參閱 [Azure 服務範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)清單。</span><span class="sxs-lookup"><span data-stu-id="98152-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>

| | |
|---|---|
|<span data-ttu-id="98152-106">**Active Directory**</span><span class="sxs-lookup"><span data-stu-id="98152-106">**Active Directory**</span></span>||
| <span data-ttu-id="98152-107">[搭配 Azure AD 的 Web 應用程式登入和登出][1]</span><span class="sxs-lookup"><span data-stu-id="98152-107">[Web app sign-in and sign-out with Azure AD][1]</span></span> | <span data-ttu-id="98152-108">使用 ADAL 程式庫將使用者登入和登出您的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="98152-108">Sign users in and out of your ASP.NET with the ADAL library.</span></span>
| <span data-ttu-id="98152-109">[使用 Azure AD 進行桌面應用程式驗證][2]</span><span class="sxs-lookup"><span data-stu-id="98152-109">[Desktop application authentication with Azure AD][2]</span></span>| <span data-ttu-id="98152-110">使用 ADAL 將 Azure AD 整合至 Windows 桌面 WPF 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98152-110">Integrate Azure AD into a Windows Desktop WPF app using ADAL.</span></span> | 
| <span data-ttu-id="98152-111">[使用 Azure AD 進行 Web API 驗證][3]</span><span class="sxs-lookup"><span data-stu-id="98152-111">[Web API authentication with Azure AD][3]</span></span> | <span data-ttu-id="98152-112">使用 Azure AD 的持有者權杖來保護 Web API。</span><span class="sxs-lookup"><span data-stu-id="98152-112">Protect a web API using bearer tokens from Azure AD.</span></span> |
|<span data-ttu-id="98152-113">**Key Vault**</span><span class="sxs-lookup"><span data-stu-id="98152-113">**Key Vault**</span></span>||
| <span data-ttu-id="98152-114">[從 Web 應用程式使用 Azure Key Vault][4]</span><span class="sxs-lookup"><span data-stu-id="98152-114">[Use Azure Key Vault from a Web Application][4]</span></span> | <span data-ttu-id="98152-115">從 Azure Key Vault 存取祕密，以便在 Web 應用程式中使用該祕密。</span><span class="sxs-lookup"><span data-stu-id="98152-115">Access a secret from an Azure Key Vault so that it can be used in your web application.</span></span> | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application