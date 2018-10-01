---
title: 開始使用 Azure 與 .NET
description: 了解您需要知道的 Azure 和 .NET 基本概念。
ms.date: 09/19/2018
ms.openlocfilehash: 89fdae6afa5c040127975de43c79d837550a9fbc
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190591"
---
# <a name="get-started-with-azure-and-net"></a>開始使用 Azure 與 .NET

本文件將概述 .NET 開發人員在開始使用 Azure 服務開發應用程式時，應該知曉的重要概念及服務。

## <a name="key-concepts"></a>重要概念

**Azure 帳戶**：Azure 帳戶是用來登入 Azure 服務 (例如 [Azure 入口網站](https://portal.azure.com)或 [Cloud Shell](https://shell.azure.com)) 的認證。 如果您沒有 Azure 帳戶，可以[建立一個免費帳戶](https://azure.microsoft.com/free/dotnet/)。

**Azure 訂用帳戶**：訂用帳戶是一個計費方案，您可以在其中建立 Azure 資源。 訂用帳戶可以是個人訂用帳戶，或是由您公司管理的企業訂用帳戶。 您的 Azure 帳戶可以與多個訂用帳戶相關聯。 在此情況下，請確定您已選取正確的訂用帳戶來建立資源。 如需詳細資訊，請參閱[了解帳戶、訂用帳戶和計費](https://docs.microsoft.com/azure/guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing)。

> [!TIP]
> 如果您有 Visual Studio 訂用帳戶，[則會有等待啟用的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)。

**資源群組**：資源群組是將 Azure 資源分組管理的方式。 在 Azure 中建立的資源會儲存在資源群組中，類似於將檔案儲存在電腦上的資料夾。

**託管**：若要在 Azure 中執行程式碼，則程式碼必須託管在服務中，而該服務必須可執行使用者提供的程式碼。

**受控服務**：Azure 會提供一些服務，讓您可以將資料或資訊提供給 Azure，然後 Azure 的實作會採取適當動作。 其中一個範例就是 Azure Blob 儲存體，當您提供檔案後，Azure 就會處理這些檔案的讀取、撰寫和保存作業。

## <a name="choosing-a-hosting-option"></a>選擇託管選項

Azure 中的託管可分為三類。

* **基礎結構即服務 (IaaS)**：有了 IaaS，您可以佈建所需要的虛擬機器，以及相關聯的網路和儲存體元件。 然後您會部署想放在這些 VM 上的任何軟體和應用程式。 此模型最接近傳統內部部署環境，不同之處在於 Microsoft 會管理基礎結構。 您還是可以管理個別的 VM，包括作業系統、自訂軟體和安全性更新。

* **平台即服務 (PaaS)**：PaaS 提供受控的託管環境，您可以在其中部署應用程式而不需要管理 VM 或網路資源。 例如，不要建立個別的 VM，您可以指定執行個體計數，而服務將會佈建、設定和管理所需的資源。 Azure App Service 是 PaaS 服務的範例。
  
* **函式即服務 (FaaS)**：FaaS 通常稱為無伺服器運算，能比 PaaS 更進一步地分擔託管環境的考量。 您不用建立計算執行個體並將程式碼部署到其中，只需部署您的程式碼，服務即會自動執行程式碼。 您也不需要管理計算資源。 平台會根據處理流量時所需的任何層級，無縫地相應增加或減少您的程式碼，而且只有當程式碼執行時才需支付費用。 Azure Functions 即是 FaaS 服務。

一般而言，如果您應用程式支援的 FaaS 和 PaaS 模型愈多，則愈能從雲端執行中看見優勢。 以下是 Azure 中三種常見託管選項的摘要及選擇時機。

* [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)：如果您想要託管 Web 應用程式或服務，請先考慮 App Service。 若要開始使用 App Service 和 ASP.NET、WCF 和 ASP.NET Core 應用程式，請參閱[在 Azure 中建立 ASP.NET Core Web 應用程式](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-dotnet)。

* [Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)：Azure Functions 非常適合由事件驅動的工作流程。 範例包括：Webhook 的回應、佇列或 Blob 儲存體中的項目處理及計時器。 若要開始使用 Azure Functions，請參閱[使用 Visual Studio 建立您的第一個函式](https://docs.microsoft.com/azure/azure-functions/functions-create-your-first-function-visual-studio)。

* [Azure 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/)：如果因為特定相依性，使得 App Service 無法符合您託管現有應用程式的需求，那麼最簡單的方式是從虛擬機器開始使用。 若要開始使用虛擬機器和 ASP.NET 或 WCF，請參閱[將 ASP.NET 應用程式部署到 Azure 虛擬機器](https://tutorials.visualstudio.com/aspnet-vm/intro)。

> [!TIP]
> 如需更完整的 Azure 服務清單，請參閱 [ Azure 計算選項的概觀](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-overview#azure-compute-options)。 如需有關服務選擇的詳細資訊，請參閱 [Azure 計算服務的決策樹](https://docs.microsoft.com/azure/architecture/guide/technology-choices/compute-decision-tree)。

## <a name="choosing-a-data-storage-service"></a>選擇資料儲存服務

根據您的需求，Azure 提供多個儲存資料的服務。 適用於 .NET 開發人員的最常見資料服務為：

* [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)：如果您想要將已使用 SQL Server 的應用程式遷移至雲端，那麼 Azure SQL Database 就是理所當然的起點。 若要開始，請參閱[教學課程：在 Azure 中搭配 SQL Database 來建置 ASP.NET 應用程式](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase)。

* [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/)；Azure Cosmos DB 是針對雲端設計的新式資料庫。 當您開始建置尚未有特定資料庫相依性的新應用程式時，應該考慮使用 Azure Cosmos DB。 對於新的 Web、行動裝置、遊戲和 IoT 應用程式，若其中自動調整規模、可預測的效能、快速回應時間，以及查詢無結構描述資料的能力都很重要，則 Cosmos DB 是個不錯的選擇。 若要開始，請參閱[教學課程：使用 SQL API 和 Azure 入口網站建置採用 Azure Cosmos DB 的 .NET 應用程式](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet)。

* [Azure Blob 儲存體](https://docs.microsoft.com/azure/storage/)：Azure Blob 儲存體最適合用於儲存和擷取大型二進位物件，例如影像、檔案和資料流。 物件存放區能讓您管理極大量非結構化資料。 若要開始，請參閱[快速入門：使用 .NET 在物件儲存體中建立 Blob](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-dotnet)。

> [!TIP]
> 如需詳細資訊，請參閱[選擇正確的資料存放區](https://docs.microsoft.com/azure/architecture/guide/technology-choices/data-store-overview)。

## <a name="diagnosing-problems-in-the-cloud"></a>診斷雲端中的問題

將您的應用程式部署至 Azure 後，可能會遇到應用程式可以在開發環境中運作，但無法在 Azure 中運作的狀況。 以下是診斷問題時適用的兩個入門方法：

* **從 Visual Studio 進行遠端偵錯**：大部分的 Azure 計算服務 (包括本文件中討論的服務) 皆支援透過 Visual Studio 進行遠端偵錯及取得記錄。 若要用您的應用程式來探索 Visual Studio 的功能，請在 Visual Studio 的快速啟動工具列 (位在右上角) 中，輸入 'Cloud Explorer' 來開啟 Cloud Explorer 工具視窗，然後在樹狀目錄中尋找您的應用程式。 如需詳細資訊，請參閱[使用 Visual Studio 對 Azure App Service 中的 Web 應用程式進行疑難排解](https://docs.microsoft.com/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio#remotedebug)。

* **Application Insights**：[Application Insights](https://docs.microsoft.com/azure/application-insights/) 是完整的應用程式效能監控 (APM) 解決方案，可自動擷取應用程式中的診斷資料、遙測和效能資料。 若要開始收集您應用程式的診斷資料，請參閱[開始監視 ASP.NET Web 應用程式](https://docs.microsoft.com/azure/application-insights/quick-monitor-portal)。

## <a name="next-steps"></a>後續步驟

* [將第一個 ASP.NET Core Web 應用程式部署至 Azure](https://docs.microsoft.com/azure/app-service/app-service-web-get-started-dotnet)
* [了解如何使用適用於.NET 的 Azure API 進行驗證](dotnet-sdk-azure-authenticate.md)
* [診斷雲端應用程式中的錯誤](https://blogs.msdn.microsoft.com/webdev/2018/02/07/diagnosing-errors-on-your-cloud-apps)
* 下載免費電子書：[適用於 .NET 開發人員的 Azure 快速入門手冊](https://www.microsoft.com/net/download/thank-you/azure-quick-start-ebook)
