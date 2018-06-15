---
title: 將 ASP.NET Web 應用程式移轉至 Azure App Service
description: 了解如何從內部部署將 ASP.NET Web 應用程式移轉至 Azure App Service。
keywords: Azure .NET, ASP.NET, App Service, Web 應用程式, 移轉, 移轉
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: 050782871c3fe4ccb0d15bf9933c3b11c88ce661
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
ms.locfileid: "29728419"
---
# <a name="migrate-an-aspnet-web-application-to-azure-app-service"></a>將 ASP.NET Web 應用程式移轉至 Azure App Service

[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) 是完全受控的計算平台服務，非常適合用來裝載可擴充的網站和 Web 應用程式。 本文件提供以下資訊：如何隨即將現有的應用程式轉移至 Azure App Service、可列入考慮的修改，以及移到雲端的其他資源。

準備好開始了嗎？ [將 ASP.NET + SQL 應用程式發佈至 Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214)。

# <a name="preparation"></a>準備工作   
* [如何判斷您的應用程式是否符合 App Service](https://azure.microsoft.com/downloads/migration-assistant/)
* [將您的資料庫移至雲端](https://go.microsoft.com/fwlink/?linkid=863217)

# <a name="considerations"></a>考量
在移轉應用程式之前，有幾個您必須考慮的因素。 以下是您可能需要對應用程式進行的修改清單，以及進行修改的方式。

## <a name="sql-database-configuration"></a>SQL Database 設定
如果您的應用程式正在使用內部部署資料庫，則 Web 應用程式有數個選項。 [深入了解將 SQL 資料庫移轉至 Azure](https://go.microsoft.com/fwlink/?linkid=863217)。

## <a name="iis"></a>IIS
傳統上透過應用程式中 applicationHost.config 設定的所有項目現在皆可透過 Azure 入口網站設定。 這適用於 AppPool 位元、啟用/停用 websocket、受控管線版本、.NET Framework 版本 (2.0/4.0) 等。若要修改[應用程式設定](https://docs.microsoft.com/azure/app-service/web-sites-configure)，瀏覽至 [Azure 入口網站](https://portal.azure.com)，開啟 Web 應用程式刀鋒視窗，然後選取 [應用程式設定] 索引標籤。

## <a name="authentication"></a>驗證
如果應用程式在任何時間點驗證使用者，則您必須修改這項功能，讓該功能在應用程式一部署到 Azure Web Apps 後即可運作。 其中一種方法是使用 Azure AD Connect 整合內部部署目錄與 Azure Active Directory。 [深入了解如何整合您的內部部署目錄與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。

## <a name="virtual-network-modification"></a>虛擬網路修改
如果您使用超過一個 Azure 服務，可以考慮使用虛擬網路在這些服務之間安全地進行通訊。 您可以使用 VPN 或 ExpressRoute 設定從內部部署網路到 [Azure 虛擬網路](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet)的連線。

## <a name="monitoring-and-diagnostics"></a>監視和診斷
您目前的監控和診斷內部部署解決方案無法在雲端中運作。 不過，Azure 提供記錄、監控和診斷工具，以便識別及偵錯 Web 應用程式的問題。 您可以輕鬆地在設定中啟用 Web 應用程式診斷，且可以檢視 Azure Application Insights 中所記的記錄。 [深入了解啟用 Web 應用程式的診斷記錄](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log)。

## <a name="connection-strings-and-application-settings"></a>連接字串和應用程式設定
讓資訊保持安全的其中一項作法是使用 [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/)，這項服務可以安全地儲存應用程式中所使用的敏感資訊。 或者，您可以將此資料儲存為 App Service 設定。

## <a name="dns"></a>DNS
您可能需要根據應用程式需求更新 DNS 設定。 這些 DNS 設定可在 App Service 的[自訂網域設定](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain)中進行設定。 要考量的另一個因素是[繫結現有的自訂 SSL 憑證](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl)。

## <a name="file-system-and-storage"></a>檔案系統和儲存體
如果您的應用程式會存留資料，您必須進行更新以使用 Azure 儲存體。 Azure 儲存體是提供檔案共用的服務，可透過 SMB 通訊協定、blob 儲存體、簡單佇列與非關聯式資料表進行共用。 [深入了解 Azure 儲存體檔案共用](https://docs.microsoft.com/azure/storage/files/storage-files-introduction)。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [將 ASP.NET Web 應用程式移轉至 Azure App Service](https://aka.ms/azure-webapp-migrate)
