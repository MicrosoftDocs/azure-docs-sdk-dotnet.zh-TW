---
title: "適用於 .NET 的 Azure 媒體服務程式庫"
description: "適用於 .NET 的 Azure 媒體服務程式庫參考"
keywords: "Azure, .NET, SDK, API, 媒體服務"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: media-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 872ed60363c0c886e9844d0cb0bef07cf41a0242
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2017
---
# <a name="azure-media-services-libraries-for-net"></a><span data-ttu-id="7eaff-104">適用於 .NET 的 Azure 媒體服務程式庫</span><span class="sxs-lookup"><span data-stu-id="7eaff-104">Azure Media Services libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7eaff-105">概觀</span><span class="sxs-lookup"><span data-stu-id="7eaff-105">Overview</span></span>

<span data-ttu-id="7eaff-106">Microsoft Azure 媒體服務是一個可延伸的雲端型平台，供開發人員建置可擴充的媒體管理和傳遞應用程式。</span><span class="sxs-lookup"><span data-stu-id="7eaff-106">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="7eaff-107">媒體服務是以 REST API 為基礎，可讓您安全地上傳、儲存、編碼和封裝視訊或音訊內容，以用於隨選和即時資料流傳遞給各種用戶端 (例如電視、電腦和行動裝置)。</span><span class="sxs-lookup"><span data-stu-id="7eaff-107">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span> 

<span data-ttu-id="7eaff-108">若要進一步了解，請參閱[概觀](/azure/media-services/media-services-overview)和 [.NET 使用者入門](/azure/media-services/media-services-dotnet-how-to-use)。</span><span class="sxs-lookup"><span data-stu-id="7eaff-108">To learn more, see [Overview](/azure/media-services/media-services-overview) and [Getting started with .NET](/azure/media-services/media-services-dotnet-how-to-use).</span></span> 

## <a name="client-library"></a><span data-ttu-id="7eaff-109">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="7eaff-109">Client library</span></span>

<span data-ttu-id="7eaff-110">Azure 媒體服務 .NET SDK 程式庫可讓您使用 .NET 對媒體服務進行程式設計。</span><span class="sxs-lookup"><span data-stu-id="7eaff-110">The Azure Media Services .NET SDK library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="7eaff-111">使用 Azure 媒體服務用戶端程式庫來連線、驗證，並針對媒體服務 API 進行開發。</span><span class="sxs-lookup"><span data-stu-id="7eaff-111">Use the Azure Media Services client library to connect, authenticate, and develop against Media Services APIs.</span></span>  

<span data-ttu-id="7eaff-112">如需詳細資訊，請參閱[使用 .NET SDK 傳遞點播內容入門](/azure/media-services/media-services-dotnet-get-started)。</span><span class="sxs-lookup"><span data-stu-id="7eaff-112">For more information, see [Get started with delivering content on demand using .NET SDK](/azure/media-services/media-services-dotnet-get-started).</span></span>

<span data-ttu-id="7eaff-113">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/windowsazure.mediaservices)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="7eaff-113">Install the [NuGet package](https://www.nuget.org/packages/windowsazure.mediaservices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7eaff-114">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="7eaff-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a><span data-ttu-id="7eaff-115">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="7eaff-115">Code Example</span></span>

<span data-ttu-id="7eaff-116">下列程式碼範例使用媒體服務 .NET SDK 執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="7eaff-116">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="7eaff-117">建立編碼工作。</span><span class="sxs-lookup"><span data-stu-id="7eaff-117">Create an encoding job.</span></span>
- <span data-ttu-id="7eaff-118">取得對 Media Encoder Standard 編碼器的參考</span><span class="sxs-lookup"><span data-stu-id="7eaff-118">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="7eaff-119">指定要使用彈性資料流預設值。</span><span class="sxs-lookup"><span data-stu-id="7eaff-119">Specify to use the Adaptive Streaming preset.</span></span>
- <span data-ttu-id="7eaff-120">將單一編碼工作加入工作。</span><span class="sxs-lookup"><span data-stu-id="7eaff-120">Add a single encoding task to the job.</span></span>
- <span data-ttu-id="7eaff-121">指定要編碼的輸入資產。</span><span class="sxs-lookup"><span data-stu-id="7eaff-121">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="7eaff-122">建立輸出資產以接收編碼資產。</span><span class="sxs-lookup"><span data-stu-id="7eaff-122">Create an output asset to receive the encoded asset.</span></span>
- <span data-ttu-id="7eaff-123">提交作業。</span><span class="sxs-lookup"><span data-stu-id="7eaff-123">Submit the job.</span></span>


```csharp
/* Include this 'using' directive:
using Microsoft.WindowsAzure.MediaServices.Client;
*/

CloudMediaContext context = new CloudMediaContext(new Uri(mediaServiceRESTAPIEndpoint), tokenProvider);

// Get an uploaded asset.
IAsset asset = context.Assets.FirstOrDefault();

// Encode and generate the output using the "Adaptive Streaming" preset.
// Declare a new job.
IJob job = context.Jobs.Create("Media Encoder Standard Job");
// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName)
    .ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();
if (processor == null) 
{
    throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));
}

// Create a task with the encoding details, using a string preset.
// In this case "Adaptive Streaming" preset is used.
ITask task = job.Tasks.AddNew("My encoding task", processor, "Adaptive Streaming", TaskOptions.None);

// Specify the input asset to be encoded.
task.InputAssets.Add(asset);
// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);

job.Submit();
job.GetExecutionProgressTask(CancellationToken.None).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7eaff-124">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="7eaff-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a><span data-ttu-id="7eaff-125">範例</span><span class="sxs-lookup"><span data-stu-id="7eaff-125">Samples</span></span>

- [<span data-ttu-id="7eaff-126">串流以 Apple FairPlay 保護的 HLS 內容</span><span class="sxs-lookup"><span data-stu-id="7eaff-126">Stream your HLS content Protected with Apple FairPlay</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [<span data-ttu-id="7eaff-127">使用 .NET SDK 延伸模組將 blob 複製到 Azure 媒體服務資產</span><span class="sxs-lookup"><span data-stu-id="7eaff-127">Copy blob into an Azure Media Services asset using .NET SDK Extensions</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [<span data-ttu-id="7eaff-128">使用 .NET SDK 搭配 Azure 媒體服務編碼和傳送即時資料流</span><span class="sxs-lookup"><span data-stu-id="7eaff-128">Encode and Deliver a Live Stream with Azure Media Services using .NET SDK</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

<span data-ttu-id="7eaff-129">檢視 Azure 媒體服務範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services)。</span><span class="sxs-lookup"><span data-stu-id="7eaff-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) of Azure Media Services samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
