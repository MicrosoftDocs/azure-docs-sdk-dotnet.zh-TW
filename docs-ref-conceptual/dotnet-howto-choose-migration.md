---
title: 選擇正確的 Azure 裝載選項
description: 了解哪些 Azure 移轉路徑適合您的 ASP.NET Web 應用程式。
author: CESARDELATORRE
ms.author: cesardl
ms.date: 11/15/2017
ms.openlocfilehash: 7c0d10436efa86c3d4a60f80e2eebd935ee01cee
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190611"
---
# <a name="choose-the-right-azure-hosting-option"></a>選擇正確的 Azure 裝載選項

本文件提供從內部部署將現有的 .NET Framework 應用程式移轉到 Azure 時，您所擁有 Azure 中多個選擇之間的眾多考量和比較。

將現有 .NET 應用程式移轉至 Azure 時要考慮的基本領域如下︰

1.  計算服務選項
2.  資料庫選項
3.  網路和安全性考量
4.  驗證和授權考量

## <a name="compute-choices"></a>計算服務選項

將現有的 .NET Framework 應用程式移轉至 Azure 時則會有多個選項。  不過，因為 .NET Framework 相依於 Windows，下列選項僅限於以 Windows 為基礎的計算服務。

下表列出數個比較和建議，可協助您為現有的 .NET 應用程式選擇適合的計算移轉路徑。

|                 | Azure VM | Azure App Service | Windows 容器 |
|-----------------|-----------|-------------------|--------------------|
|使用時機      |<ul><li>應用程式在伺服器和本機 .msi 安裝上具有強烈相依性。</li><li>您希望應用程式移轉路徑越簡單越好</li></ul>|應用程式與伺服器沒有相依性，是個乾淨的 ASP.NET Web 應用程式 (MVC、WebForm) 或存取資料庫伺服器的多層式架構應用程式 (Web API、WCf)。 |<ul><li>應用程式在原始伺服器上具有相依性，但這些相依性可以包含在 Docker Windows 映像中。</li><li>想要將應用程式現代化，使其可使用[雲端 DevOps](https://docs.microsoft.com/dotnet/standard/modernize-with-azure-and-containers/lift-and-shift-existing-apps-devops/reasons-to-lift-and-shift-existing-net-apps-to-cloud-devops-ready-applications)</li></ul>|
|優點與好處  |<ul><li>最簡單的移轉路徑</li><li>熟悉的環境。 部署環境是與內部部署伺服器非常類似的 VM。</li></ul> |進行中的 PaaS 維護作業是在 Azure 中管理和調整應用程式最簡單的方式。 |<ul><li>已備妥供日後使用，具相依性的雲端 DevOps 就緒包含在應用程式的容器中。</li><li>幾乎不需要重新建構 .NET /C# 程式碼。</li></ul> |
|缺點             |此為 IaaS。 維護成本昂貴。 您需要管理 VM 基礎結構的網路、負載平衡器、擴充、IIS 管理等等。 |<ul><li>並未[支援](http://www.migratetoazure.net/ReadinessAssessment)所有的應用程式</li><li>某些應用程式可能需要重構並稍微重新架構，才能支援 Azure App Service。</li></ul> |<ul><li>Docker 的技能學習曲線</li><li>某些程式碼和應用程式組態設定會變更</li></ul>|
|需求 |比起內部部署應用程式，具有相同需求的 Windows Server VM | 在 [Azure App Service 相容性分析](https://www.migratetoazure.net/Resources)中指定的 Azure App Service 需求。 |<ul><li>[Windows Server 2016 with Containers - Azure VM](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview)<br />或</li><li>[Azure Container Service (AKS)](https://azure.microsoft.com/services/container-service/) (此為 Kubernetes 協調器)<br />或<li>[Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) 協調器</li></ul> |
|如何移轉 |請參閱[移轉至 Azure 虛擬機器](https://go.microsoft.com/fwlink/?linkid=862531) | 請參閱[移轉 Azure App Service](https://go.microsoft.com/fwlink/?linkid=862532) | 請依照[將現有 .NET 應用程式與 Azure 和 Windows 容器現代化電子書](https://aka.ms/liftandshiftwithcontainersebook)中說明的考量、案例和逐步解說 |

 下列流程圖顯示了為您現有 .NET Framework 應用程式規劃移轉至 Azure 時的決策樹，選項 A 若可行則為第一個可嘗試執行的選項，但選項 B 為最簡單的執行路徑。

![顯示裝載決策樹的流程圖](media/dotnet-howto-choose-migration/decision-tree.png)

## <a name="database-choices"></a>資料庫選項

將關聯式資料庫移轉到 Azure 時您有多個選項。 請參閱[將 SQL Server 資料庫移轉至 Azure](https://go.microsoft.com/fwlink/?linkid=862533)，可協助您為現有的 .NET 應用程式選擇正確的資料庫移轉路徑。

## <a name="networking-and-security-considerations"></a>網路和安全性考量

在將應用程式部署至如 Microsoft Azure 等公用雲端時，您可能想要[建立網路 DMZ](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/) 來隔離和保護特定網路，例如 [Azure 與內部部署間的 DMZ](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) 或 [Azure 與網際網路間的 DMZ](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz)。 DMZ 可以透過 [Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview)來實作。
Azure 虛擬網路可讓您：

- 建置可控制的混合式基礎結構
- 使用自己的 IP 位址與 DNS 伺服器
- 利用 IPsec VPN 或 ExpressRoute 保障連線的安全
- 對子網路間的流量進行細微的控制
- 使用虛擬應用設備建立精密的網路拓撲
- 為應用程建立獨立且極為安全的應用程式環境
 
若要開始建置您自己的虛擬網路，請參閱 [Azure 虛擬網路文件](https://docs.microsoft.com/azure/virtual-network/)。

## <a name="authentication-and-authorization-considerations-when-migrating-to-azure"></a>移轉至 Azure 時的驗證和授權考量

任何組織要移到雲端時的首要考量皆是安全性。 大部分的公司投資了大量時間、金錢和工程來設計和開發安全性模型，重要的是，這些公司能夠充分利用現有投資，例如身分識別存放區和單一登入解決方案。

許多執行於內部部署的現有企業 B2E .NET 應用程式使用 Active Directory 進行驗證和身分識別管理。  Azure AD Connect 可讓您整合內部部署目錄與 Azure Active Directory。  若要開始，請參閱[整合您的內部部署目錄與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。

請參閱[混合式身分識別解決方案的身分識別需求](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-business-needs)以進一步進行 Azure Active Directory 的相關規劃。

其他驗證通訊協定的選擇還有 [OAuth](https://en.wikipedia.org/wiki/OAuth) 和 [OpenID](https://en.wikipedia.org/wiki/OpenID)，其在消費者導向應用程式中很常見。  使用自發的身分識別資料庫 (例如由 IdentityServer4 使用 OAuth 包裝的 ASP.NET 身分識別 SQL 資料庫)，通常不需連線到內部部署資料庫或目錄。

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [將 ASP.NET Web 應用程式移轉至 Azure App Service](dotnet-howto-migrate-app-service.md)