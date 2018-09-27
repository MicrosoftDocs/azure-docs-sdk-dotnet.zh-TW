---
title: 保護 Azure 應用程式的 .NET 教學課程
description: 在 Azure 上執行之 .NET 應用程式的應用程式安全性和身分識別管理教學課程。
ms.date: 10/19/2017
ms.openlocfilehash: 19960efa8faa762f0cde657d702f09a8dcb66e99
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190641"
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a>驗證在 Azure 上執行之 .NET 應用程式的使用者教學課程

下表連結到驗證使用者和保護在 Azure 上執行之 .NET 應用程式的深入教學課程。

如需範例原始程式碼，請參閱 [Azure 服務範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)清單。

| | |
|---|---|
|**Active Directory**||
| [使用 Visual Studio 連線服務將 Azure Active Directory 新增至 Web 應用程式][5] | 將 Web 應用程式連線至 Visual Studio 中的 Azure AD |
| [搭配 Azure AD 的 Web 應用程式登入和登出][1] | 使用 ADAL 程式庫將使用者登入和登出您的 ASP.NET。 |
| [使用 Azure AD 進行桌面應用程式驗證][2]| 使用 ADAL 將 Azure AD 整合至 Windows 桌面 WPF 應用程式。 | 
| [使用 Azure AD 進行 Web API 驗證][3] | 使用 Azure AD 的持有者權杖來保護 Web API。 |
|**金鑰保存庫**||
| [使用 Visual Studio 連線服務在 Web 應用程式中新增 Key Vault][6] | 將 Web 應用程式連線至 Visual Studio 中的 Azure Key Vault |
| [從 Web 應用程式使用 Azure Key Vault][4] | 從 Azure Key Vault 存取祕密，以便在 Web 應用程式中使用該祕密。 | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service