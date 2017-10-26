---
title: "適用於 .NET 範例指示的 Azure 管理程式庫"
description: "取得程式碼範例，以使用適用於 .NET 的 Azure 管理程式庫來建立和更新資源。"
keywords: "Azure, .NET, SDK, API, 範例, 範例"
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
ms.openlocfilehash: cf5195bbc64ae39917355e3b775afa0c46604c4a
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a>適用於 .NET 範例指示的 Azure 管理程式庫

本文說明執行適用於 .NET 的 Azure 管理程式庫範例所需的必要條件和驗證。

## <a name="prerequisties"></a>必要條件 

* [Visual Studio 2017](https://www.visualstudio.com/vs/) 或 [.NET Core SDK](https://www.microsoft.com/net/download/core)
* [Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/)
* [Git 命令列用戶端](https://git-scm.com/)
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

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