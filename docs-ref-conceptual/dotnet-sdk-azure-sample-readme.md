---
title: 適用於 .NET 範例指示的 Azure 管理程式庫
description: 取得程式碼範例，以使用適用於 .NET 的 Azure 管理程式庫來建立和更新資源。
keywords: Azure, .NET, SDK, API, 範例, 範例
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a931e623768e1fddad263c7da8eb864c37613379
ms.sourcegitcommit: 9dd801d659803f5efb16d65454cd09258e1cc7d6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2018
ms.locfileid: "29752470"
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a><span data-ttu-id="123a1-104">適用於 .NET 範例指示的 Azure 管理程式庫</span><span class="sxs-lookup"><span data-stu-id="123a1-104">Azure management libraries for .NET sample instructions</span></span>

<span data-ttu-id="123a1-105">本文說明執行適用於 .NET 的 Azure 管理程式庫範例所需的必要條件和驗證。</span><span class="sxs-lookup"><span data-stu-id="123a1-105">This article describes the prerequisites and authentication required for running the samples for the Azure management libraries for .NET.</span></span>

## <a name="prerequisties"></a><span data-ttu-id="123a1-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="123a1-106">Prerequisties</span></span> 

* <span data-ttu-id="123a1-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) 或 [.NET Core SDK](https://www.microsoft.com/net/download/core)</span><span class="sxs-lookup"><span data-stu-id="123a1-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) or [.NET Core SDK](https://www.microsoft.com/net/download/core)</span></span>
* <span data-ttu-id="123a1-108">[Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="123a1-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="123a1-109">Git 命令列用戶端</span><span class="sxs-lookup"><span data-stu-id="123a1-109">Git command line client</span></span>](https://git-scm.com/)
* [<span data-ttu-id="123a1-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="123a1-110">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a><span data-ttu-id="123a1-111">驗證所有範例</span><span class="sxs-lookup"><span data-stu-id="123a1-111">Authentication for all samples</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a><span data-ttu-id="123a1-112">執行範例</span><span class="sxs-lookup"><span data-stu-id="123a1-112">Running the samples</span></span>

<span data-ttu-id="123a1-113">在已使用 Git 複製此範例後，您便可以在 Visual Studio 中開啟範例，並使用 IDE 執行範例。</span><span class="sxs-lookup"><span data-stu-id="123a1-113">Once you have used Git to clone the sample, you can open the sample in Visual Studio and run the sample using the IDE.</span></span>  <span data-ttu-id="123a1-114">或者，使用 .NET Core SDK 從命令列來建置及執行範例，就像這樣：</span><span class="sxs-lookup"><span data-stu-id="123a1-114">Alternatively, use the .NET Core SDK to build and run the sample from the command line, like this:</span></span>

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```