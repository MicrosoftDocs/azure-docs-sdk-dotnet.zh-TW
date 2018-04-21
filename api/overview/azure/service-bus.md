---
title: 適用於 .NET 的 Azure 服務匯流排程式庫
description: 適用於 .NET 的 Azure 服務匯流排程式庫參考
keywords: Azure, .NET, SDK, API, 服務匯流排
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f2795a123a7b92237b0aea672298ce9339fd0830
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2018
---
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="512d9-104">適用於 .NET 的 Azure 服務匯流排程式庫</span><span class="sxs-lookup"><span data-stu-id="512d9-104">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="512d9-105">概觀</span><span class="sxs-lookup"><span data-stu-id="512d9-105">Overview</span></span>

<span data-ttu-id="512d9-106">[Azure 服務匯流排](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)是座落在應用程式之間的訊息基礎結構，可讓應用程式交換訊息以增進規模和恢復功能。</span><span class="sxs-lookup"><span data-stu-id="512d9-106">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="512d9-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="512d9-107">Client library</span></span>

<span data-ttu-id="512d9-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus)。</span><span class="sxs-lookup"><span data-stu-id="512d9-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="512d9-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="512d9-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="512d9-110">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="512d9-110">Code Example</span></span>

<span data-ttu-id="512d9-111">這個範例會將訊息傳送至服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="512d9-111">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="512d9-112">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="512d9-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="512d9-113">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="512d9-113">Management library</span></span>

<span data-ttu-id="512d9-114">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="512d9-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="512d9-115">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="512d9-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="512d9-116">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="512d9-116">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="512d9-117">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="512d9-117">Code Example</span></span>

<span data-ttu-id="512d9-118">這個範例會建立服務匯流排佇列，大小上限為 1024 MB。</span><span class="sxs-lookup"><span data-stu-id="512d9-118">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

```csharp
// using Microsoft.Azure.Management.ServiceBus.Fluent;
// using Microsoft.Azure.Management.ServiceBus.Fluent.Models;

using (ServiceBusManagementClient client = new ServiceBusManagementClient(credentials))
{
    client.SubscriptionId = subscriptionId;
    QueueInner parameters = new QueueInner
    {
        MaxSizeInMegabytes = 1024
    };
    await client.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, queueName, parameters);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="512d9-119">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="512d9-119">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="512d9-120">範例</span><span class="sxs-lookup"><span data-stu-id="512d9-120">Samples</span></span>

- [<span data-ttu-id="512d9-121">服務匯流排基本 - .Net</span><span class="sxs-lookup"><span data-stu-id="512d9-121">Service Bus Queue Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [<span data-ttu-id="512d9-122">服務匯流排進階功能 - .Net</span><span class="sxs-lookup"><span data-stu-id="512d9-122">Service Bus Queue Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [<span data-ttu-id="512d9-123">服務匯流排發佈/訂閱基本 - .Net</span><span class="sxs-lookup"><span data-stu-id="512d9-123">Service Bus Publish/Subscribe Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [<span data-ttu-id="512d9-124">服務匯流排發佈/訂閱進階功能 - .Net</span><span class="sxs-lookup"><span data-stu-id="512d9-124">Service Bus Publish/Subscribe Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [<span data-ttu-id="512d9-125">具宣告式授權的服務匯流排 - .Net</span><span class="sxs-lookup"><span data-stu-id="512d9-125">Service Bus with Claims-Based Authorization - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

<span data-ttu-id="512d9-126">檢視 Azure 服務匯流排範例的[完整清單](https://azure.microsoft.com/resources/samples/?term=service+bus)。</span><span class="sxs-lookup"><span data-stu-id="512d9-126">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
