---
title: Azure .NET API
description: 適用於 .NET 的 Azure API 概觀
keywords: Azure, .NET, SDK, API, NuGet, 程式庫, 套件
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 26360a516220ca9d3e8901e60cb23ecbd02863cd
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
---
# <a name="azure-net-apis"></a><span data-ttu-id="17288-104">Azure .NET API</span><span class="sxs-lookup"><span data-stu-id="17288-104">Azure .NET APIs</span></span>

<span data-ttu-id="17288-105">Azure .NET API 可讓您使用 Azure 服務，並從應用程式程式碼管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="17288-105">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="17288-106">API 可作為 [NuGet 套件](/dotnet/api/overview/azure/)，在 .NET 專案中使用。</span><span class="sxs-lookup"><span data-stu-id="17288-106">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="17288-107">管理 Azure 資源</span><span class="sxs-lookup"><span data-stu-id="17288-107">Manage Azure resources</span></span>

<span data-ttu-id="17288-108">適用於 .NET 的 Azure 程式庫可讓您從 .NET 應用程式建立並管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="17288-108">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="17288-109">許多管理 Azure 資源的套件都有 [Fluent](dotnet-sdk-azure-concepts.md) 介面，可完全以您的規格設定資源。</span><span class="sxs-lookup"><span data-stu-id="17288-109">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="17288-110">例如，若要建立 Windows VM，您需要撰寫下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="17288-110">For example, to create a Windows VM you would write the following code:</span></span>

```csharp
var windowsVM = azure.VirtualMachines.Define(windowsVmName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername(username)
    .WithAdminPassword(password)
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
 ```

<span data-ttu-id="17288-111">檢閱 [.NET 服務清單](/dotnet/api/overview/azure/)，立即開始使用程式庫與您的專案。</span><span class="sxs-lookup"><span data-stu-id="17288-111">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="17288-112">然後讀取[開始使用文章](dotnet-sdk-azure-get-started.md)，針對您自己的 Azure 訂用帳戶設定驗證並執行範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="17288-112">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="17288-113">[概念文件](dotnet-sdk-azure-concepts.md)會討論 SDK 所使用的慣例，以及如何利用它們來簡化您的應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="17288-113">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="17288-114">新功能、重大變更以及移轉的指示則會在[版本資訊](dotnet-sdk-azure-release-notes.md)中提供。</span><span class="sxs-lookup"><span data-stu-id="17288-114">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="17288-115">取用 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="17288-115">Consume Azure services</span></span>

<span data-ttu-id="17288-116">除了可以使用 .NET API 來建立 Azure 內的資源並以程式設計方式加以管理，您也可以使用 .NET API 將應用程式連線到這些資源，並在執行階段使用它們。</span><span class="sxs-lookup"><span data-stu-id="17288-116">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="17288-117">例如，您可以連線到 SQL Database，或在 Azure 儲存體內儲存資料。</span><span class="sxs-lookup"><span data-stu-id="17288-117">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="17288-118">您可以瀏覽[服務 API 的完整清單](/dotnet/api/overview/azure/)，來識別要用於特定 Azure 服務的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="17288-118">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="17288-119">範例</span><span class="sxs-lookup"><span data-stu-id="17288-119">Samples</span></span>

<span data-ttu-id="17288-120">下列範例涵蓋常見的自動化工作，並包含適用於 .NET 的 Azure 程式庫：</span><span class="sxs-lookup"><span data-stu-id="17288-120">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="17288-121">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="17288-121">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="17288-122">Web Apps</span><span class="sxs-lookup"><span data-stu-id="17288-122">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="17288-123">SQL Database</span><span class="sxs-lookup"><span data-stu-id="17288-123">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="17288-124">我們提供了一個適用於服務和管理程式庫中所有套件的統一[參考](/dotnet/api/overview/azure/?view=azure-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="17288-124">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="17288-125">新功能、重大變更以及移轉的指示則會在[版本資訊](dotnet-sdk-azure-release-notes.md)中提供。</span><span class="sxs-lookup"><span data-stu-id="17288-125">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]