---
title: "保護 Azure 應用程式的 .NET 教學課程"
description: "在 Azure 上執行之 .NET 應用程式的應用程式安全性和身分識別管理教學課程。"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 0cd530ef5f70778571e2f702aebc4a8b43c40e93
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2017
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a>驗證在 Azure 上執行之 .NET 應用程式的使用者教學課程

下表連結到驗證使用者和保護在 Azure 上執行之 .NET 應用程式的深入教學課程。

如需範例原始程式碼，請參閱 [Azure 服務範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)清單。

| | |
|---|---|
|**Active Directory**||
| [搭配 Azure AD 的 Web 應用程式登入和登出][1] | 使用 ADAL 程式庫將使用者登入和登出您的 ASP.NET。
| [使用 Azure AD 進行桌面應用程式驗證][2]| 使用 ADAL 將 Azure AD 整合至 Windows 桌面 WPF 應用程式。 | 
| [使用 Azure AD 進行 Web API 驗證][3] | 使用 Azure AD 的持有者權杖來保護 Web API。 |
|**金鑰保存庫**||
| [從 Web 應用程式使用 Azure Key Vault][4] | 從 Azure Key Vault 存取祕密，以便在 Web 應用程式中使用該祕密。 | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application