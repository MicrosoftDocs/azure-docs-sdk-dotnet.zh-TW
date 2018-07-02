---
title: 適用於 .NET 的 Azure Event Grid 程式庫
description: 適用於 .NET 的 Azure Event Grid 程式庫參考
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/16/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: event-grid
ms.custom: devcenter
ms.openlocfilehash: 922e1a49a2b864d8cd408a8383d7cda27c7f89c2
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065298"
---
# <a name="azure-event-grid-libraries-for-net"></a><span data-ttu-id="9bc7d-103">適用於 .NET 的 Azure Event Grid 程式庫</span><span class="sxs-lookup"><span data-stu-id="9bc7d-103">Azure Event Grid libraries for .NET</span></span>

<span data-ttu-id="9bc7d-104">建置事件導向的應用程式會傾聽並回應來自 Azure 服務和自訂來源的事件，這些事件會使用由 Azure Event Grid 處理的簡單型事件。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-104">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="9bc7d-105">[進一步了解 ](/azure/event-grid/overview)Azure Event Grid 的相關資訊，並參考 [Azure Blob 儲存體教學課程](/azure/storage/blobs/storage-blob-event-quickstart-powershell)開始使用。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="9bc7d-106">發佈 SDK</span><span class="sxs-lookup"><span data-stu-id="9bc7d-106">Publish SDK</span></span>

<span data-ttu-id="9bc7d-107">使用 Azure Event Grid 發佈 SDK 來建立事件、驗證並發佈至主題。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-107">Create events, authenticate, and post to topics using the Azure Event Grid publish SDK.</span></span>

<span data-ttu-id="9bc7d-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9bc7d-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9bc7d-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="9bc7d-110">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="9bc7d-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="sample-usage"></a><span data-ttu-id="9bc7d-111">範例用法</span><span class="sxs-lookup"><span data-stu-id="9bc7d-111">Sample usage</span></span>

<span data-ttu-id="9bc7d-112">下列程式碼會向 Azure 進行驗證，並將自訂類型的 `EventGridEvent` 事件 `List` (在本範例中為 `Contoso.Items.ItemsReceivedEvent`) 發佈至主題。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-112">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceivedEvent` ) to a topic.</span></span> <span data-ttu-id="9bc7d-113">您可以從 Azure PowerShell 中擷取範例中使用的主題金鑰和端點位址：</span><span class="sxs-lookup"><span data-stu-id="9bc7d-113">The topic key and endpoint address used in the sample can be retrieved from Azure PowerShell:</span></span>

```powershell
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name <topic-name>).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name <topic-name>
```

```csharp
string topicEndpoint = "https://<topic-name>.<region>-1.eventgrid.azure.net/api/events";
string topicKey = "<topic-key>";
string topicHostname = new Uri(topicEndpoint).Host;

TopicCredentials topicCredentials = new TopicCredentials(topicKey);
EventGridClient client = new EventGridClient(topicCredentials);

client.PublishEventsAsync(topicHostname, GetEventsList()).GetAwaiter().GetResult();
Console.Write("Published events to Event Grid.");

static IList<EventGridEvent> GetEventsList()
{
    List<EventGridEvent> eventsList = new List<EventGridEvent>();
    for (int i = 0; i < 1; i++)
    {
        eventsList.Add(new EventGridEvent()
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Contoso.Items.ItemReceivedEvent",
            Data = new ContosoItemReceivedEventData()
            {
                ItemUri = "ContosoSuperItemUri"
            },

            EventTime = DateTime.Now,
            Subject = "Door1",
            DataVersion = "2.0"
        });
    }
    return eventsList;
}
```

<span data-ttu-id="9bc7d-114">此程式碼片段會在 [Azure 儲存體](/azure/storage/blobs/storage-blob-event-overview)中建立新 Blob 時，處理已發佈的事件。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-114">This snippet handles events published when creating a new blob in [Azure Storage](/azure/storage/blobs/storage-blob-event-overview).</span></span>

```csharp
string response = string.Empty;
const string SubscriptionValidationEvent = "Microsoft.EventGrid.SubscriptionValidationEvent";
const string StorageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";

string requestContent = await req.Content.ReadAsStringAsync();
EventGridEvent[] eventGridEvents = JsonConvert.DeserializeObject<EventGridEvent[]>(requestContent);

foreach (EventGridEvent eventGridEvent in eventGridEvents)
{
    JObject dataObject = eventGridEvent.Data as JObject;

    // Deserialize the event data into the appropriate type based on event type 
    if (string.Equals(eventGridEvent.EventType, SubscriptionValidationEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<SubscriptionValidationEventData>();
        log.Info($"Got SubscriptionValidation event data, validation code: {eventData.ValidationCode}, topic: {eventGridEvent.Topic}");

        // Do any additional validation (as required) and then return back the below response
        var responseData = new SubscriptionValidationResponseData();
        responseData.ValidationResponse = eventData.ValidationCode;
        return req.CreateResponse(HttpStatusCode.OK, responseData);
    }

    else if (string.Equals(eventGridEvent.EventType, StorageBlobCreatedEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<StorageBlobCreatedEventData>();
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9bc7d-115">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="9bc7d-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="9bc7d-116">管理 SDK</span><span class="sxs-lookup"><span data-stu-id="9bc7d-116">Management SDK</span></span>

<span data-ttu-id="9bc7d-117">透過管理 SDK 來建立、更新或刪除 Event Grid 執行個體、主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-117">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

<span data-ttu-id="9bc7d-118">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="9bc7d-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9bc7d-119">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="9bc7d-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="9bc7d-120">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="9bc7d-120">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9bc7d-121">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="9bc7d-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="9bc7d-122">深入了解</span><span class="sxs-lookup"><span data-stu-id="9bc7d-122">Learn more</span></span>

- [<span data-ttu-id="9bc7d-123">使用 Event Grid SDK 接收事件</span><span class="sxs-lookup"><span data-stu-id="9bc7d-123">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
