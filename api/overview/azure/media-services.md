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
# <a name="azure-media-services-libraries-for-net"></a>適用於 .NET 的 Azure 媒體服務程式庫

## <a name="overview"></a>概觀

Microsoft Azure 媒體服務是一個可延伸的雲端型平台，供開發人員建置可擴充的媒體管理和傳遞應用程式。 媒體服務是以 REST API 為基礎，可讓您安全地上傳、儲存、編碼和封裝視訊或音訊內容，以用於隨選和即時資料流傳遞給各種用戶端 (例如電視、電腦和行動裝置)。 

若要進一步了解，請參閱[概觀](/azure/media-services/media-services-overview)和 [.NET 使用者入門](/azure/media-services/media-services-dotnet-how-to-use)。 

## <a name="client-library"></a>用戶端程式庫

Azure 媒體服務 .NET SDK 程式庫可讓您使用 .NET 對媒體服務進行程式設計。 使用 Azure 媒體服務用戶端程式庫來連線、驗證，並針對媒體服務 API 進行開發。  

如需詳細資訊，請參閱[使用 .NET SDK 傳遞點播內容入門](/azure/media-services/media-services-dotnet-get-started)。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/windowsazure.mediaservices)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a>程式碼範例

下列程式碼範例使用媒體服務 .NET SDK 執行下列工作：

- 建立編碼工作。
- 取得對 Media Encoder Standard 編碼器的參考
- 指定要使用彈性資料流預設值。
- 將單一編碼工作加入工作。
- 指定要編碼的輸入資產。
- 建立輸出資產以接收編碼資產。
- 提交作業。


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
> [探索用戶端 API](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a>範例

- [串流以 Apple FairPlay 保護的 HLS 內容](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [使用 .NET SDK 延伸模組將 blob 複製到 Azure 媒體服務資產](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [使用 .NET SDK 搭配 Azure 媒體服務編碼和傳送即時資料流](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

檢視 Azure 媒體服務範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services)。


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
