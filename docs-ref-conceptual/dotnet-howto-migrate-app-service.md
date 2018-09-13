---
title: 將您的 .NET Web 應用程式或服務遷移至 Azure App Service
description: 了解如何從內部部署將 .NET Web 應用程式或服務遷移至 Azure App Service。
keywords: Azure .NET, ASP.NET, WCF, App Service, Web 應用程式, 遷移, 移轉
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 07/16/2018
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: af17a7dee8dd93aa50807b0b6b7eebadb673151b
ms.sourcegitcommit: 6a1974bc7c7511aacac5b69daa296a59ab3f8000
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/12/2018
ms.locfileid: "44700950"
---
# <a name="migrate-your-net-web-app-or-service-to-azure-app-service"></a><span data-ttu-id="cc564-104">將您的 .NET Web 應用程式或服務遷移至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cc564-104">Migrate your .NET web app or service to Azure App Service</span></span> 

<span data-ttu-id="cc564-105">[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) 是完全受控的計算平台服務，非常適合用來裝載可擴充的網站和 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc564-105">[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) is a fully-managed compute platform service that is optimized for hosting scalable websites and web applications.</span></span> <span data-ttu-id="cc564-106">本文件提供以下資訊：如何隨即將現有的應用程式轉移至 Azure App Service、可列入考慮的修改，以及移到雲端的其他資源。</span><span class="sxs-lookup"><span data-stu-id="cc564-106">This document provides information on how to lift-and-shift an existing application to Azure App Service, modifications to consider, and additional resources for moving to the cloud.</span></span> <span data-ttu-id="cc564-107">大部分 ASP.NET 網站 (Webforms、MVC) 和服務 (Web API、WCF) 都可以在沒有變更的情況下直接移至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="cc564-107">Most ASP.NET websites (Webforms, MVC) and services (Web API, WCF) can move directly to Azure App Service with no changes.</span></span> <span data-ttu-id="cc564-108">一些服務可能需要些微變更，而其他服務則可能需要進行一些重構。</span><span class="sxs-lookup"><span data-stu-id="cc564-108">Some may need minor changes while others may need some refactoring.</span></span>

<span data-ttu-id="cc564-109">準備好開始了嗎？</span><span class="sxs-lookup"><span data-stu-id="cc564-109">Ready to get started?</span></span> <span data-ttu-id="cc564-110">[將 ASP.NET + SQL 應用程式發佈至 Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214)。</span><span class="sxs-lookup"><span data-stu-id="cc564-110">[Publish your ASP.NET + SQL application to Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).</span></span>

## <a name="considerations"></a><span data-ttu-id="cc564-111">考量</span><span class="sxs-lookup"><span data-stu-id="cc564-111">Considerations</span></span>

### <a name="on-premises-resources-including-sql-server"></a><span data-ttu-id="cc564-112">內部部署資源 (包括 SQL Server)</span><span class="sxs-lookup"><span data-stu-id="cc564-112">On-premises resources (including SQL Server)</span></span>

<span data-ttu-id="cc564-113">因為內部部署資源可能需要遷移或變更，所以請確認內部部署資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="cc564-113">Verify access to on-premises resources as these may need to be migrated or changed.</span></span> <span data-ttu-id="cc564-114">減少內部部署資源存取權的選項如下：</span><span class="sxs-lookup"><span data-stu-id="cc564-114">The following are options for mitigating access to on-premises resources:</span></span>

* <span data-ttu-id="cc564-115">使用 [Azure 虛擬網路](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet)建立 VPN，讓 App Service 與內部部署資源連線。</span><span class="sxs-lookup"><span data-stu-id="cc564-115">Create a VPN connecting App Service to on-premises resources using [Azure Virtual Networks](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet).</span></span>
* <span data-ttu-id="cc564-116">使用 [Azure 轉送](https://docs.microsoft.com/azure/service-bus-relay/relay-what-is-it)安全地將內部部署服務公開至雲端，而不變更防火牆。</span><span class="sxs-lookup"><span data-stu-id="cc564-116">Securely expose on-premises services to the cloud without firewall changes using [Azure Relay](https://docs.microsoft.com/azure/service-bus-relay/relay-what-is-it).</span></span>
* <span data-ttu-id="cc564-117">將例如 [SQL 資料庫](https://go.microsoft.com/fwlink/?linkid=863217) 的相依性遷移至 Azure。</span><span class="sxs-lookup"><span data-stu-id="cc564-117">Migrate dependencies such as a [SQL database](https://go.microsoft.com/fwlink/?linkid=863217) to Azure.</span></span>
* <span data-ttu-id="cc564-118">在雲端中使用平台即服務供應項目，來減少相依性。</span><span class="sxs-lookup"><span data-stu-id="cc564-118">Use platform-as-a-service offerings in the cloud to reduce dependecies.</span></span> <span data-ttu-id="cc564-119">例如，請考慮使用 [SendGrid](https://docs.microsoft.com/azure/sendgrid-dotnet-how-to-send-email)，而不是連線到內部部署郵件伺服器。</span><span class="sxs-lookup"><span data-stu-id="cc564-119">For example, rather than connect to an on-premises mail server, consider using [SendGrid](https://docs.microsoft.com/azure/sendgrid-dotnet-how-to-send-email).</span></span> 

### <a name="port-bindings"></a><span data-ttu-id="cc564-120">連接埠繫結</span><span class="sxs-lookup"><span data-stu-id="cc564-120">Port Bindings</span></span>

<span data-ttu-id="cc564-121">Azure App Service 支援連接埠 80 (適用於 HTTP) 和連接埠 443 (適用於 HTTPS 流量)。</span><span class="sxs-lookup"><span data-stu-id="cc564-121">Azure App Service supports port 80 for HTTP and port 443 for HTTPS traffic.</span></span>

<span data-ttu-id="cc564-122">針對 WCF，支援下列繫結：</span><span class="sxs-lookup"><span data-stu-id="cc564-122">For WCF, the following bindings are supported:</span></span>

<span data-ttu-id="cc564-123">繫結</span><span class="sxs-lookup"><span data-stu-id="cc564-123">Binding</span></span> | <span data-ttu-id="cc564-124">注意</span><span class="sxs-lookup"><span data-stu-id="cc564-124">Notes</span></span>
--------|--------
<span data-ttu-id="cc564-125">BasicHttp</span><span class="sxs-lookup"><span data-stu-id="cc564-125">BasicHttp</span></span> | 
<span data-ttu-id="cc564-126">WSHttp</span><span class="sxs-lookup"><span data-stu-id="cc564-126">WSHttp</span></span> | 
<span data-ttu-id="cc564-127">WSDualHttpBinding</span><span class="sxs-lookup"><span data-stu-id="cc564-127">WSDualHttpBinding</span></span> | <span data-ttu-id="cc564-128">必須啟用 [Web 通訊端支援](https://docs.microsoft.com/azure/app-service/web-sites-configure)。</span><span class="sxs-lookup"><span data-stu-id="cc564-128">[Web socket support](https://docs.microsoft.com/azure/app-service/web-sites-configure) must be enabled.</span></span>
<span data-ttu-id="cc564-129">NetHttpBinding</span><span class="sxs-lookup"><span data-stu-id="cc564-129">NetHttpBinding</span></span> | <span data-ttu-id="cc564-130">必須針對雙面合約啟用 [Web 通訊端支援](https://docs.microsoft.com/azure/app-service/web-sites-configure)。</span><span class="sxs-lookup"><span data-stu-id="cc564-130">[Web socket support](https://docs.microsoft.com/azure/app-service/web-sites-configure) must be enabled for duplex contracts.</span></span>
<span data-ttu-id="cc564-131">NetHttpsBinding</span><span class="sxs-lookup"><span data-stu-id="cc564-131">NetHttpsBinding</span></span> | <span data-ttu-id="cc564-132">必須針對雙面合約啟用 [Web 通訊端支援](https://docs.microsoft.com/azure/app-service/web-sites-configure)。</span><span class="sxs-lookup"><span data-stu-id="cc564-132">[Web socket support](https://docs.microsoft.com/azure/app-service/web-sites-configure) must be enabled for duplex contracts.</span></span>
<span data-ttu-id="cc564-133">BasicHttpContextBinding</span><span class="sxs-lookup"><span data-stu-id="cc564-133">BasicHttpContextBinding</span></span> |
<span data-ttu-id="cc564-134">WebHttpBinding</span><span class="sxs-lookup"><span data-stu-id="cc564-134">WebHttpBinding</span></span> |
<span data-ttu-id="cc564-135">WSHttpContextBinding</span><span class="sxs-lookup"><span data-stu-id="cc564-135">WSHttpContextBinding</span></span> |

### <a name="authentication"></a><span data-ttu-id="cc564-136">驗證</span><span class="sxs-lookup"><span data-stu-id="cc564-136">Authentication</span></span>

<span data-ttu-id="cc564-137">Azure App Service 預設支援匿名驗證，在想要使用時支援表單驗證。</span><span class="sxs-lookup"><span data-stu-id="cc564-137">Azure App Service supports anonymous authentication by default and Forms authentication when intended.</span></span> <span data-ttu-id="cc564-138">只有與 Azure Active Directory 和 ADFS 整合，才能使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="cc564-138">Windows authentication can be used by integrating with Azure Active Directory and ADFS only.</span></span> <span data-ttu-id="cc564-139">[深入了解如何整合您的內部部署目錄與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="cc564-139">[Learn more about how to integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>

### <a name="assemblies-in-the-gac-global-assembly-cache"></a><span data-ttu-id="cc564-140">GAC (全域組件快取) 中的組件</span><span class="sxs-lookup"><span data-stu-id="cc564-140">Assemblies in the GAC (Global Assembly Cache)</span></span> 

<span data-ttu-id="cc564-141">不支援此做法。</span><span class="sxs-lookup"><span data-stu-id="cc564-141">This isn't supported.</span></span> <span data-ttu-id="cc564-142">請考慮將必要組件複製到應用程式的 `\bin` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="cc564-142">Consider copying required assemblies to the app's `\bin` folder.</span></span> <span data-ttu-id="cc564-143">無法使用安裝在伺服器上的自訂 .MSI (例如 PDF 產生器等等)。</span><span class="sxs-lookup"><span data-stu-id="cc564-143">Custom .MSIs installed on the server (e.g. PDF generators, etc.) cannot be used.</span></span>  

### <a name="iis-settings"></a><span data-ttu-id="cc564-144">IIS 設定</span><span class="sxs-lookup"><span data-stu-id="cc564-144">IIS settings</span></span>
<span data-ttu-id="cc564-145">傳統上透過應用程式中 applicationHost.config 設定的所有項目現在皆可透過 Azure 入口網站設定。</span><span class="sxs-lookup"><span data-stu-id="cc564-145">Everything traditionally configured via applicationHost.config in your application can now be configured through the Azure portal.</span></span> <span data-ttu-id="cc564-146">這適用於 AppPool 位元、啟用/停用 websocket、受控管線版本、.NET Framework 版本 (2.0/4.0) 等。若要修改[應用程式設定](https://docs.microsoft.com/azure/app-service/web-sites-configure)，瀏覽至 [Azure 入口網站](https://portal.azure.com)，開啟 Web 應用程式刀鋒視窗，然後選取 [應用程式設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cc564-146">This applies to AppPool bitness, enable/disable websockets, managed pipeline version, .NET Framework version (2.0/4.0), etc. To modify your [application settings](https://docs.microsoft.com/azure/app-service/web-sites-configure), navigate to the [Azure portal](https://portal.azure.com), open the blade for your web app, and then select the **Application Settings** tab.</span></span>

#### <a name="iis5-compatibility-mode"></a><span data-ttu-id="cc564-147">IIS5 相容性模式</span><span class="sxs-lookup"><span data-stu-id="cc564-147">IIS5 Compatibility Mode</span></span>
<span data-ttu-id="cc564-148">不支援 IIS5 相容性模式。</span><span class="sxs-lookup"><span data-stu-id="cc564-148">IIS5 Compatibility Mode is not supported.</span></span> <span data-ttu-id="cc564-149">在 Azure App Service 中，每個 Web 應用程式和其下的所有應用程式都會在相同背景工作處理序中執行，具有特定的一組[應用程式集區](http://technet.microsoft.com/library/cc735247(v=WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc564-149">In Azure App Service each Web App and all of the applications under it run in the same worker process with a specific set of [application pool](http://technet.microsoft.com/library/cc735247(v=WS.10).aspx).</span></span>

#### <a name="iis7-schema-compliance"></a><span data-ttu-id="cc564-150">IIS7+ 結構描述合規性</span><span class="sxs-lookup"><span data-stu-id="cc564-150">IIS7+ schema compliance</span></span>  
<span data-ttu-id="cc564-151">部分元素和屬性未在 Azure App Service IIS 結構描述中定義。</span><span class="sxs-lookup"><span data-stu-id="cc564-151">Some elements and attributes are not defined in the Azure App Service IIS schema.</span></span> <span data-ttu-id="cc564-152">如果您遇到問題，請考慮使用 [XDT 轉換](http://azure.microsoft.com/documentation/articles/web-sites-transform-extend/)。</span><span class="sxs-lookup"><span data-stu-id="cc564-152">If you encounter issues, consider using [XDT transforms](http://azure.microsoft.com/documentation/articles/web-sites-transform-extend/).</span></span>

#### <a name="single-application-pool-per-site"></a><span data-ttu-id="cc564-153">每個網站單一應用程式集區</span><span class="sxs-lookup"><span data-stu-id="cc564-153">Single application pool per site</span></span>  
<span data-ttu-id="cc564-154">在 Azure App Service 中，每個 Web 應用程式和其下的所有應用程式都會在相同應用程式集區中執行。</span><span class="sxs-lookup"><span data-stu-id="cc564-154">In Azure App Service each Web App and all of the applications under it run in the same application pool.</span></span> <span data-ttu-id="cc564-155">請考慮建立具有通用設定的單一應用程式集區，或者為每個應用程式建立個別的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc564-155">Consider establishing a single application pool with common settings or creating a separate Web App for each application.</span></span>

### <a name="com-and-com-components"></a><span data-ttu-id="cc564-156">COM 和 COM+ 元件</span><span class="sxs-lookup"><span data-stu-id="cc564-156">COM and COM+ components</span></span>  
<span data-ttu-id="cc564-157">Azure App Service 不允許在平台上註冊 COM 元件。</span><span class="sxs-lookup"><span data-stu-id="cc564-157">Azure App Service does not allow the registration of COM components on the platform.</span></span> <span data-ttu-id="cc564-158">如果應用程式使用任何 COM 元件，則必須以受控程式碼重新撰寫這些元件，並利用網站或應用程式進行部署。</span><span class="sxs-lookup"><span data-stu-id="cc564-158">If your app makes use of any COM components, these would need to be rewritten in managed code and deployed with the site or application.</span></span>  

### <a name="physical-directories"></a><span data-ttu-id="cc564-159">實體目錄</span><span class="sxs-lookup"><span data-stu-id="cc564-159">Physical directories</span></span> 
<span data-ttu-id="cc564-160">Azure App Service 不允許實體磁碟存取。</span><span class="sxs-lookup"><span data-stu-id="cc564-160">Azure App Service does not allow physical drive access.</span></span> <span data-ttu-id="cc564-161">您可能需要使用 [Azure 檔案](https://docs.microsoft.com/azure/storage/files/storage-files-introduction)透過 SMB 存取檔案。</span><span class="sxs-lookup"><span data-stu-id="cc564-161">You may need to use a [Azure Files](https://docs.microsoft.com/azure/storage/files/storage-files-introduction) to access files via SMB.</span></span> <span data-ttu-id="cc564-162">[Azure Blob 儲存體](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction)可以儲存檔案，以供透過 HTTPS 存取。</span><span class="sxs-lookup"><span data-stu-id="cc564-162">[Azure Blob Storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction) can store files for access via HTTPS.</span></span>  

### <a name="isapi-filters"></a><span data-ttu-id="cc564-163">ISAPI 篩選</span><span class="sxs-lookup"><span data-stu-id="cc564-163">ISAPI Filters</span></span>  
<span data-ttu-id="cc564-164">Azure App Service 支援使用 ISAPI 篩選；不過，ISAPI DLL 必須部署到您的網站，並透過 web.config 註冊。</span><span class="sxs-lookup"><span data-stu-id="cc564-164">Azure App Service can support the use of ISAPI Filters, however, the ISAPI DLL must be deployed with your site and registered via web.config.</span></span>  

### <a name="https-bindings-and-ssl"></a><span data-ttu-id="cc564-165">HTTPS 繫結和 SSL</span><span class="sxs-lookup"><span data-stu-id="cc564-165">HTTPS bindings and SSL</span></span> 
<span data-ttu-id="cc564-166">HTTPS 繫結將不會遷移，SSL 憑證也不會與您的網站相關聯。</span><span class="sxs-lookup"><span data-stu-id="cc564-166">HTTPS bindings will not be migrated, nor will the SSL certificates associated with your web sites.</span></span> <span data-ttu-id="cc564-167">但是，在網站移轉完成之後，[可以手動上傳 SSL 憑證](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl)。</span><span class="sxs-lookup"><span data-stu-id="cc564-167">[SSL certificates can be manually uploaded](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl) after site migration is completed, however.</span></span>  

### <a name="sharepoint-and-frontpage"></a><span data-ttu-id="cc564-168">SharePoint 和 FrontPage</span><span class="sxs-lookup"><span data-stu-id="cc564-168">SharePoint and FrontPage</span></span> 
<span data-ttu-id="cc564-169">不支援 SharePoint 和 FrontPage Server Extensions (FPSE)。</span><span class="sxs-lookup"><span data-stu-id="cc564-169">SharePoint and FrontPage Server Extensions (FPSE) are not supported.</span></span>

### <a name="web-site-size"></a><span data-ttu-id="cc564-170">網站大小</span><span class="sxs-lookup"><span data-stu-id="cc564-170">Web site size</span></span>  
<span data-ttu-id="cc564-171">可用網站具有 1 GB 內容的大小限制。</span><span class="sxs-lookup"><span data-stu-id="cc564-171">Free sites have a size limit of 1 GB of content.</span></span> <span data-ttu-id="cc564-172">如果您的網站大於 1 GB，您必須升級為付費 SKU。</span><span class="sxs-lookup"><span data-stu-id="cc564-172">If your site is greater than 1 GB, you must upgrade to a paid SKU.</span></span> <span data-ttu-id="cc564-173">請參閱 [App Service 定價](https://azure.microsoft.com/pricing/details/app-service/windows/)。</span><span class="sxs-lookup"><span data-stu-id="cc564-173">See [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/windows/).</span></span> 

### <a name="database-size"></a><span data-ttu-id="cc564-174">資料庫大小</span><span class="sxs-lookup"><span data-stu-id="cc564-174">Database size</span></span>  
<span data-ttu-id="cc564-175">針對 SQL Server 資料庫，請參閱目前的 [SQL Database 定價](http://azure.microsoft.com/pricing/details/sql-database)。</span><span class="sxs-lookup"><span data-stu-id="cc564-175">For SQL Server databases, please check the current [SQL Database pricing](http://azure.microsoft.com/pricing/details/sql-database).</span></span>  

### <a name="azure-active-directory-aad-integration"></a><span data-ttu-id="cc564-176">Azure Active Directory (AAD) 整合</span><span class="sxs-lookup"><span data-stu-id="cc564-176">Azure Active Directory (AAD) integration</span></span>  
<span data-ttu-id="cc564-177">AAD 無法使用免費應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc564-177">AAD does not work with free apps.</span></span> <span data-ttu-id="cc564-178">若要使用 AAD，您必須升級應用程式 SKU。</span><span class="sxs-lookup"><span data-stu-id="cc564-178">To use AAD, you must upgrade the app SKU.</span></span> <span data-ttu-id="cc564-179">請參閱 [App Service 定價](https://azure.microsoft.com/pricing/details/app-service/windows/)。</span><span class="sxs-lookup"><span data-stu-id="cc564-179">See [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/windows/).</span></span>

### <a name="monitoring-and-diagnostics"></a><span data-ttu-id="cc564-180">監視和診斷</span><span class="sxs-lookup"><span data-stu-id="cc564-180">Monitoring and Diagnostics</span></span>
<span data-ttu-id="cc564-181">您目前的監控和診斷內部部署解決方案無法在雲端中運作。</span><span class="sxs-lookup"><span data-stu-id="cc564-181">Your current on-premises solutions for monitoring and diagnostics are unlikely to work in the cloud.</span></span> <span data-ttu-id="cc564-182">不過，Azure 提供記錄、監控和診斷工具，以便識別及偵錯 Web 應用程式的問題。</span><span class="sxs-lookup"><span data-stu-id="cc564-182">However, Azure provides tools for logging, monitoring, and diagnostics so that you can identify and debug issues with web apps.</span></span> <span data-ttu-id="cc564-183">您可以輕鬆地在設定中啟用 Web 應用程式診斷，且可以檢視 Azure Application Insights 中所記的記錄。</span><span class="sxs-lookup"><span data-stu-id="cc564-183">You can easily enable diagnostics for your web app in its configuration, and you can view the logs recorded in Azure Application Insights.</span></span> <span data-ttu-id="cc564-184">[深入了解啟用 Web 應用程式的診斷記錄](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log)。</span><span class="sxs-lookup"><span data-stu-id="cc564-184">[Learn more about enabling diagnostics logging for web apps](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).</span></span>

### <a name="connection-strings-and-application-settings"></a><span data-ttu-id="cc564-185">連接字串和應用程式設定</span><span class="sxs-lookup"><span data-stu-id="cc564-185">Connection Strings and application settings</span></span>
<span data-ttu-id="cc564-186">請考慮使用 [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/)，這項服務可以安全地儲存應用程式中所使用的敏感資訊。</span><span class="sxs-lookup"><span data-stu-id="cc564-186">Consider using [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), a service that securely stores sensitive information used in your application.</span></span> <span data-ttu-id="cc564-187">或者，您可以將此資料儲存為 App Service 設定。</span><span class="sxs-lookup"><span data-stu-id="cc564-187">Alternatively, you can store this data as an App Service setting.</span></span>

### <a name="dns"></a><span data-ttu-id="cc564-188">DNS</span><span class="sxs-lookup"><span data-stu-id="cc564-188">DNS</span></span>
<span data-ttu-id="cc564-189">您可能需要根據應用程式需求更新 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="cc564-189">You may need to update DNS configurations based on the requirements of your application.</span></span> <span data-ttu-id="cc564-190">這些 DNS 設定可在 App Service 的[自訂網域設定](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain)中進行設定。</span><span class="sxs-lookup"><span data-stu-id="cc564-190">These DNS settings can be configured in the App Service [custom domain settings](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain).</span></span> 

## <a name="azure-app-service-with-windows-containers"></a><span data-ttu-id="cc564-191">Azure App Service 與 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="cc564-191">Azure App Service with Windows Containers</span></span>
<span data-ttu-id="cc564-192">如果您的應用程式無法直接遷移至 App Service，請考慮使用 Windows 容器的 App Service，它可以使用 GAC、COM 元件、MSI 並完整存取 .NET FX API、DirectX 等等。</span><span class="sxs-lookup"><span data-stu-id="cc564-192">If your app cannot be migrated directly to App Service, consider App Service using Windows Containers, which enables usage of the GAC, COM components, MSIs, full access to .NET FX APIs, DirectX, and more.</span></span>

## <a name="additional-reading"></a><span data-ttu-id="cc564-193">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="cc564-193">Additional Reading</span></span>

* [<span data-ttu-id="cc564-194">如何判斷您的應用程式是否符合 App Service</span><span class="sxs-lookup"><span data-stu-id="cc564-194">How to determine if your app qualifies for App Service</span></span>](https://azure.microsoft.com/downloads/migration-assistant/)
* [<span data-ttu-id="cc564-195">將您的資料庫移至雲端</span><span class="sxs-lookup"><span data-stu-id="cc564-195">Moving your database to the cloud</span></span>](https://go.microsoft.com/fwlink/?linkid=863217)
* [<span data-ttu-id="cc564-196">Azure Web 應用程式沙箱詳細資訊和限制</span><span class="sxs-lookup"><span data-stu-id="cc564-196">Azure Web App sandbox details and restrictions</span></span>](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox)

## <a name="next-steps"></a><span data-ttu-id="cc564-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc564-197">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc564-198">將 ASP.NET Web 應用程式移轉至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cc564-198">Migrate an ASP.NET Web application to Azure App Service</span></span>](https://aka.ms/azure-webapp-migrate)
