---
title: "適用於 .NET 範例指示的 Azure 管理程式庫"
description: "取得程式碼範例，以使用適用於 .NET 的 Azure 管理程式庫來建立和更新資源。"
keywords: "Azure, .NET, SDK, API, 範例, 範例"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: ffda7cca724962e6f953432c5cab04485ddabb03
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a>適用於 .NET 範例指示的 Azure 管理程式庫

本文說明執行適用於 .NET 的 Azure 管理程式庫範例所需的必要條件和驗證。

## <a name="prerequisties"></a>必要條件 

* [Visual Studio 2017](https://www.visualstudio.com/vs/) 或 [.NET Core SDK](https://www.microsoft.com/net/download/core)
* [Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/)
* [Git 命令列用戶端](https://git-scm.com/)
* [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a>驗證所有範例

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a>執行範例

在已使用 Git 複製此範例後，您便可以在 Visual Studio 中開啟範例，並使用 IDE 執行範例。  或者，使用 .NET Core SDK 從命令列來建置及執行範例，就像這樣：

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```