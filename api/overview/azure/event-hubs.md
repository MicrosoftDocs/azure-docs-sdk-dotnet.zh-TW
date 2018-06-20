---
title: 適用於 .NET 的 Azure 事件中樞程式庫
description: 適用於 .NET 的 Azure 事件中樞程式庫參考
keywords: Azure, .NET, SDK, API, 事件中樞
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: event-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2ec234959ffc46d2399d1c763e05f173a311b0d2
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487291"
---
# <a name="azure-event-hubs-libraries-for-net"></a><span data-ttu-id="f59a8-104">適用於 .NET 的 Azure 事件中樞程式庫</span><span class="sxs-lookup"><span data-stu-id="f59a8-104">Azure Event Hubs libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="f59a8-105">概觀</span><span class="sxs-lookup"><span data-stu-id="f59a8-105">Overview</span></span>

<span data-ttu-id="f59a8-106">Azure 事件中樞為可高度擴充的資料串流平台和事件擷取服務。</span><span class="sxs-lookup"><span data-stu-id="f59a8-106">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service.</span></span>

<span data-ttu-id="f59a8-107">若要了解有關 Azure 事件中樞的詳細資訊，請參閱文章[何謂事件中樞？](/azure/event-hubs/event-hubs-what-is-event-hubs)。</span><span class="sxs-lookup"><span data-stu-id="f59a8-107">To learn more about Azure Event Hubs, read the article [What is Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>  <span data-ttu-id="f59a8-108">若要開始使用，請參閱[事件中樞程式設計指南](/azure/event-hubs/event-hubs-programming-guide)。</span><span class="sxs-lookup"><span data-stu-id="f59a8-108">To get started, check out the [Event Hubs Programming Guide](/azure/event-hubs/event-hubs-programming-guide).</span></span>

## <a name="client-library"></a><span data-ttu-id="f59a8-109">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="f59a8-109">Client library</span></span>

<span data-ttu-id="f59a8-110">使用事件中樞用戶端來傳送和接收事件中樞的訊息。</span><span class="sxs-lookup"><span data-stu-id="f59a8-110">Use the Event Hubs client to send and receive messages to and from Event Hubs.</span></span>

<span data-ttu-id="f59a8-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.EventHubs)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="f59a8-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f59a8-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="f59a8-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a><span data-ttu-id="f59a8-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="f59a8-113">Code Example</span></span>

<span data-ttu-id="f59a8-114">下列程式碼會建立事件中樞用戶端，並將訊息傳送至中樞。</span><span class="sxs-lookup"><span data-stu-id="f59a8-114">The following code creates an Event Hubs client and sends a message to the hub.</span></span>

```csharp
EventHubsConnectionStringBuilder connectionStringBuilder = new EventHubsConnectionStringBuilder(eventHubConnectionString)
{
    EntityPath = eventHubEntityPath
};

EventHubClient eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
string message = $"Message {i}";
Console.WriteLine($"Sending message: {message}");
await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f59a8-115">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="f59a8-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a><span data-ttu-id="f59a8-116">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="f59a8-116">Management library</span></span>

<span data-ttu-id="f59a8-117">使用事件中樞管理程式庫來建立、更新及移除中樞和取用者群組。</span><span class="sxs-lookup"><span data-stu-id="f59a8-117">Use the Event Hubs management library to create, update, and remove hubs and consumer groups.</span></span>

<span data-ttu-id="f59a8-118">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="f59a8-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f59a8-119">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="f59a8-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a><span data-ttu-id="f59a8-120">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="f59a8-120">Code Example</span></span>

<span data-ttu-id="f59a8-121">下列程式碼會建立新的中樞。</span><span class="sxs-lookup"><span data-stu-id="f59a8-121">The following code creates a new event hub.</span></span>

```csharp
TokenCredentials creds = new TokenCredentials(token);
EventHubManagementClient ehClient = new EventHubManagementClient(creds)
{
    SubscriptionId = subscriptionId
};

EventHubCreateOrUpdateParameters ehParams = new EventHubCreateOrUpdateParameters()
{
    Location = location
};

Console.WriteLine("Creating Event Hub...");
await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
Console.WriteLine("Created Event Hub successfully.");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f59a8-122">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="f59a8-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a><span data-ttu-id="f59a8-123">教學課程</span><span class="sxs-lookup"><span data-stu-id="f59a8-123">Tutorials</span></span>

* [<span data-ttu-id="f59a8-124">使用 .NET Framework 將事件傳送至 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="f59a8-124">Send events to Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [<span data-ttu-id="f59a8-125">使用 .NET Framework 從 Azure 事件中樞接收事件</span><span class="sxs-lookup"><span data-stu-id="f59a8-125">Receive events from Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a><span data-ttu-id="f59a8-126">範例</span><span class="sxs-lookup"><span data-stu-id="f59a8-126">Samples</span></span>

* [<span data-ttu-id="f59a8-127">Azure 事件中樞範例</span><span class="sxs-lookup"><span data-stu-id="f59a8-127">Azure Event Hubs Samples</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="f59a8-128">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="f59a8-128">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
