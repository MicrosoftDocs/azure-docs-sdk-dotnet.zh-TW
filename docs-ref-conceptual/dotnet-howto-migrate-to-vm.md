---
title: 將 ASP.NET Web 應用程式移轉至 Azure 虛擬機器
description: 了解如何從內部部署將 ASP.NET Web 應用程式移轉至 Azure 虛擬機器。
ms.date: 11/15/2017
ms.service: virtual-machines
ms.openlocfilehash: b33bffdf774688d9d7eb5947f1a080b021ba259c
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190701"
---
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a><span data-ttu-id="710ad-103">將 ASP.NET Web 應用程式移轉至 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="710ad-103">Migrate an ASP.NET Web application to an Azure Virtual Machine</span></span>

<span data-ttu-id="710ad-104">此文件說明了如何從內部部署將 ASP.NET Web 應用程式移轉至 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="710ad-104">This document provides an overview of how to migrate an ASP.NET web application from on-premises to an Azure Virtual Machine.</span></span>

## <a name="quickstart"></a><span data-ttu-id="710ad-105">快速入門</span><span class="sxs-lookup"><span data-stu-id="710ad-105">Quickstart</span></span>

<span data-ttu-id="710ad-106">了解如何建立虛擬機器，並將您的應用程式發佈到該虛擬機器中：[發佈至 Azure VM](https://tutorials.visualstudio.com/aspnet-vm/intro)</span><span class="sxs-lookup"><span data-stu-id="710ad-106">Learn how to create a virtual machine and publish your app to it: [Publish to an Azure VM](https://tutorials.visualstudio.com/aspnet-vm/intro)</span></span>

## <a name="get-started"></a><span data-ttu-id="710ad-107">開始使用</span><span class="sxs-lookup"><span data-stu-id="710ad-107">Get Started</span></span>

<span data-ttu-id="710ad-108">這些教學課程會示範建立 (或移轉) 虛擬機器的步驟，如何將 Web 應用程式發佈至其中，以及 Azure 中其他可能需要用以支援應用程式的工作。</span><span class="sxs-lookup"><span data-stu-id="710ad-108">These tutorials demonstrate the steps to create (or migrate) a virtual machine, publish your web application to it, and other tasks that may be required to support your application in Azure.</span></span>

- <span data-ttu-id="710ad-109">使用下列兩選項的其中一個在 Azure 中建立 ASP.NET 應用程式的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="710ad-109">Create a virtual machine for your ASP.NET application in Azure using one of the following two options:</span></span>
    - [<span data-ttu-id="710ad-110">為 ASP.NET 應用程式建立新的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="710ad-110">Create a new virtual machine for ASP.NET Applications</span></span>](https://go.microsoft.com/fwlink/?linkid=863237)
    - [<span data-ttu-id="710ad-111">移轉現有的內部部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="710ad-111">Migrate an existing on-premises virtual machine</span></span>](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [<span data-ttu-id="710ad-112">使用 Visual Studio 發佈您的應用程式</span><span class="sxs-lookup"><span data-stu-id="710ad-112">Publish your app using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?linkid=863240)
- [<span data-ttu-id="710ad-113">建立 VM 的安全虛擬網路</span><span class="sxs-lookup"><span data-stu-id="710ad-113">Create a secure virtual network for your VMs</span></span>](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [<span data-ttu-id="710ad-114">建立應用程式的 CI/CD 管線</span><span class="sxs-lookup"><span data-stu-id="710ad-114">Create a CI/CD pipeline for your application</span></span>](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [<span data-ttu-id="710ad-115">為高可用性和延展性移至虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="710ad-115">Move to a VM scale set for high availability and scalability</span></span>](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a><span data-ttu-id="710ad-116">考量</span><span class="sxs-lookup"><span data-stu-id="710ad-116">Considerations</span></span>

### <a name="benefits"></a><span data-ttu-id="710ad-117">優點</span><span class="sxs-lookup"><span data-stu-id="710ad-117">Benefits</span></span>

<span data-ttu-id="710ad-118">虛擬機器提供了從內部部署將應用程式移轉至雲端最簡單的路徑。</span><span class="sxs-lookup"><span data-stu-id="710ad-118">Virtual machines offer the easiest path to migrate an application from on-premises to the cloud.</span></span>  <span data-ttu-id="710ad-119">可讓您複寫應用程式在內部部署中使用的相同環境，且不需維護自己的資料中心。</span><span class="sxs-lookup"><span data-stu-id="710ad-119">They enable you to replicate the same environment your application uses on-premises, while removing the need to maintain your own data centers.</span></span>  <span data-ttu-id="710ad-120">虛擬機器擴展集針對在虛擬機器中執行的應用程式提供高可用性和延展性。</span><span class="sxs-lookup"><span data-stu-id="710ad-120">Virtual Machine Scale Sets provide high availability and scalability for applications running in Virtual Machines.</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="710ad-121">虛擬機器大小</span><span class="sxs-lookup"><span data-stu-id="710ad-121">Virtual Machine Size</span></span>

<span data-ttu-id="710ad-122">針對您的工作負載選擇最佳化的虛擬機器大小和類型。</span><span class="sxs-lookup"><span data-stu-id="710ad-122">Choose the virtual machine size and type that is best optimized for your workload.</span></span>  <span data-ttu-id="710ad-123">如需詳細資訊，請參閱＜[Azure 中 Windows 虛擬機器的大小](https://docs.microsoft.com/azure/virtual-machines/windows/sizes)＞。</span><span class="sxs-lookup"><span data-stu-id="710ad-123">See [sizes for Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) for more information.</span></span>

### <a name="maintenance"></a><span data-ttu-id="710ad-124">維護 </span><span class="sxs-lookup"><span data-stu-id="710ad-124">Maintenance</span></span>

<span data-ttu-id="710ad-125">正如同內部部署機器，您必須負責維護和更新虛擬機器 <sup>&#42;</sup>。</span><span class="sxs-lookup"><span data-stu-id="710ad-125">Just like an on-premises machine, you are responsible for maintaining and updating the virtual machine<sup>&#42;</sup>.</span></span>  <span data-ttu-id="710ad-126">如果您的應用程式可以在平台即服務 (PaaS) 環境中執行，如 [Azure App Service](https://docs.microsoft.com/azure/app-service/) 或[容器](https://docs.microsoft.com/azure/app-service/containers/)，則將會移除這項需求。</span><span class="sxs-lookup"><span data-stu-id="710ad-126">If your application can run in a Platform as a Service (PaaS) environment such as [Azure App Service](https://docs.microsoft.com/azure/app-service/) or in a [container](https://docs.microsoft.com/azure/app-service/containers/), that will remove this need.</span></span>

<span data-ttu-id="710ad-127"><sup>&#42;</sup>[虛擬機器擴展集的自動作業系統升級](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade)目前可提供預覽服務。</span><span class="sxs-lookup"><span data-stu-id="710ad-127">*<sup>&#42;</sup>[Automatic OS upgrades for virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) is currently available as a Preview service.*</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="710ad-128">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="710ad-128">Virtual Networks</span></span>

<span data-ttu-id="710ad-129">Azure 虛擬網路可讓您：</span><span class="sxs-lookup"><span data-stu-id="710ad-129">Azure Virtual Networks enable you to:</span></span>
- <span data-ttu-id="710ad-130">建置可控制的混合式基礎結構</span><span class="sxs-lookup"><span data-stu-id="710ad-130">Build a hybrid infrastructure that you control</span></span>
- <span data-ttu-id="710ad-131">使用自己的 IP 位址與 DNS 伺服器</span><span class="sxs-lookup"><span data-stu-id="710ad-131">Bring your own IP addresses and DNS servers</span></span>
- <span data-ttu-id="710ad-132">建立獨立且極為安全的應用程式環境</span><span class="sxs-lookup"><span data-stu-id="710ad-132">Create an isolated and highly-secure environment for your applications</span></span>
- <span data-ttu-id="710ad-133">使用其中一種[連線選項](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)將 VM 連線至內部部署網路</span><span class="sxs-lookup"><span data-stu-id="710ad-133">Connect your VM to your on-premises network using one of several [connectivity options](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span></span>
- <span data-ttu-id="710ad-134">使用 [ExpressRoute](https://azure.microsoft.com/services/expressroute/) 將您的虛擬機器整合到內部部署網路</span><span class="sxs-lookup"><span data-stu-id="710ad-134">Integrate your virtual machine into your on-premises network using [ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span></span>

<span data-ttu-id="710ad-135">請參閱[虛擬網路文件](https://docs.microsoft.com/azure/virtual-network/)以開始使用</span><span class="sxs-lookup"><span data-stu-id="710ad-135">To get started, see the [Virtual Network documentation](https://docs.microsoft.com/azure/virtual-network/)</span></span>

### <a name="active-directory"></a><span data-ttu-id="710ad-136">Active Directory</span><span class="sxs-lookup"><span data-stu-id="710ad-136">Active Directory</span></span>
<span data-ttu-id="710ad-137">許多應用程式使用 Active Directory 進行驗證和身分識別管理。</span><span class="sxs-lookup"><span data-stu-id="710ad-137">Many applications use Active Directory for authentication and identity management.</span></span>  
- <span data-ttu-id="710ad-138">Azure AD Connect 可讓您整合內部部署目錄與 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="710ad-138">Azure AD Connect enables you to integrate your on-premises directories with Azure Active Directory.</span></span>  <span data-ttu-id="710ad-139">若要開始，請參閱[整合您的內部部署目錄與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="710ad-139">To get started, see [Integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>  
- <span data-ttu-id="710ad-140">或者，[ExpressRoute](https://azure.microsoft.com/services/expressroute/) 可讓應用程式存取您的內部部署 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="710ad-140">Alternatively, [ExpressRoute](https://azure.microsoft.com/services/expressroute/) enables your application to access your on-premises Active Directory.</span></span>

### <a name="sql-databases"></a><span data-ttu-id="710ad-141">SQL Database</span><span class="sxs-lookup"><span data-stu-id="710ad-141">SQL Databases</span></span>

<span data-ttu-id="710ad-142">如果您的應用程式正在使用內部部署資料庫，則預設應用程式將無法與其通話。</span><span class="sxs-lookup"><span data-stu-id="710ad-142">If your application is using an on-premises database, your app will not be able to talk to it by default.</span></span> <span data-ttu-id="710ad-143">您可以：</span><span class="sxs-lookup"><span data-stu-id="710ad-143">You can either:</span></span>
- <span data-ttu-id="710ad-144">設定混合式網路，讓應用程式存取您在內部部署執行的資料庫。</span><span class="sxs-lookup"><span data-stu-id="710ad-144">Configure a hybrid network that enables your application to access your database running on-premises.</span></span>  
- <span data-ttu-id="710ad-145">將資料庫移轉至 Azure。</span><span class="sxs-lookup"><span data-stu-id="710ad-145">Migrate your database to the Azure.</span></span>  <span data-ttu-id="710ad-146">如需詳細資訊，請參閱[將 SQL Server 資料庫移轉至 Azure](dotnet-howto-migrate-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="710ad-146">See [Migrate your SQL Server database to Azure](dotnet-howto-migrate-sql.md) for more information.</span></span>

### <a name="high-availability-and-scalability"></a><span data-ttu-id="710ad-147">高可用性和延展性</span><span class="sxs-lookup"><span data-stu-id="710ad-147">High Availability and Scalability</span></span>

#### <a name="virtual-machine-scale-sets"></a><span data-ttu-id="710ad-148">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="710ad-148">Virtual Machine Scale Sets</span></span>
<span data-ttu-id="710ad-149">若您想要確定應用程式為高可用性且可以調整，可以將 VM 映像移轉到 Azure 虛擬機器擴展集來改善應用程式的可用性和延展性。</span><span class="sxs-lookup"><span data-stu-id="710ad-149">You want to make sure that your application is highly available and can scale, migrate your VM image to an Azure Virtual Machine Scale Set to improve the availability and scalability of your application.</span></span>  <span data-ttu-id="710ad-150">VM 擴展集提供功能可讓您使用已設定的現有 VM，或設定組建管線來建置應用程式的映像。</span><span class="sxs-lookup"><span data-stu-id="710ad-150">VM Scale Sets provide the ability to use an existing VM you’ve already configured or set up a build pipeline to build an image with your application.</span></span>  

<span data-ttu-id="710ad-151">若要開始，請參閱[在虛擬機器擴展集上部署您的應用程式](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)。</span><span class="sxs-lookup"><span data-stu-id="710ad-151">To get started, see [Deploy your application on virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span></span>

#### <a name="centralized-logging"></a><span data-ttu-id="710ad-152">集中式記錄</span><span class="sxs-lookup"><span data-stu-id="710ad-152">Centralized Logging</span></span>
<span data-ttu-id="710ad-153">在多個執行個體中執行應用程式時，請考慮將您的記錄儲存在集中位置，如 [Azure 儲存體](https://docs.microsoft.com/azure/storage/)。</span><span class="sxs-lookup"><span data-stu-id="710ad-153">When running your application across multiple instances, consider storing your logs in a centralized location such as [Azure Storage](https://docs.microsoft.com/azure/storage/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="710ad-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="710ad-154">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="710ad-155">將 SQL Server 資料庫移轉到 Azure</span><span class="sxs-lookup"><span data-stu-id="710ad-155">Migrate a SQL Server database to Azure</span></span>](dotnet-howto-migrate-sql.md)