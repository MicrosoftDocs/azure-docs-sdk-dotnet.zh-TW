---
title: "在 Azure 上使用 .NET 傳訊和 IoT 的教學課程 | Microsoft Docs"
description: "使用 .NET 和 Azure 服務在雲端應用程式之間以及在裝置與雲端之間傳送訊息。"
author: camsoper
manager: douge
ms.assetid: 2ce6ea06-7b0b-45e6-8ca0-44e4e4030b82
ms.devlang: dotnet
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: casoper
ms.openlocfilehash: 0c3e81231ac88b2418778b83ecabcbb553608e24
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="net-tutorials-for-enterprise-messaging-and-internet-of-things-iot"></a><span data-ttu-id="513ab-103">企業傳訊和物聯網 (IoT) 的 .NET 教學課程</span><span class="sxs-lookup"><span data-stu-id="513ab-103">.NET tutorials for enterprise messaging and Internet of Things (IoT)</span></span>

<span data-ttu-id="513ab-104">下表連線至在 .NET 程式碼中使用 Azure 服務來傳送和讀取應用程式和裝置之間訊息的深入教學課程。</span><span class="sxs-lookup"><span data-stu-id="513ab-104">The following table links to in-depth tutorials for sending and reading messages between applications and devices in from your .NET code using Azure services.</span></span>

<span data-ttu-id="513ab-105">如需範例原始程式碼，請參閱 [Azure 服務範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)清單。</span><span class="sxs-lookup"><span data-stu-id="513ab-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>


| | |
|---|---|
| <span data-ttu-id="513ab-106">**服務匯流排**</span><span class="sxs-lookup"><span data-stu-id="513ab-106">**Service Bus**</span></span> | |
| <span data-ttu-id="513ab-107">[如何使用服務匯流排佇列][1]</span><span class="sxs-lookup"><span data-stu-id="513ab-107">[How to use Service Bus queues][1]</span></span> | <span data-ttu-id="513ab-108">建立佇列、傳送和接收訊息，以及刪除佇列。</span><span class="sxs-lookup"><span data-stu-id="513ab-108">Create queues, send and receive messages, and delete queues.</span></span> | 
| <span data-ttu-id="513ab-109">[如何使用服務匯流排主題和訂閱][2]</span><span class="sxs-lookup"><span data-stu-id="513ab-109">[How to use Service Bus topics and subscriptions][2]</span></span> | <span data-ttu-id="513ab-110">了解如何搭配服務匯流排使用發佈/訂閱通訊模型。</span><span class="sxs-lookup"><span data-stu-id="513ab-110">Learn how to use publish/subscribe communication model with Service Bus.</span></span>
| <span data-ttu-id="513ab-111">[搭配使用 .NET 的服務匯流排與 AMQP 1.0][3]</span><span class="sxs-lookup"><span data-stu-id="513ab-111">[Using Service Bus from .NET with AMQP 1.0][3]</span></span> | <span data-ttu-id="513ab-112">了解如何在您的服務匯流排應用程式中使用 AMQP。</span><span class="sxs-lookup"><span data-stu-id="513ab-112">Learn how to use AMQP in you Service Bus applications.</span></span>
|<span data-ttu-id="513ab-113">**IoT 中心**</span><span class="sxs-lookup"><span data-stu-id="513ab-113">**IoT Hub**</span></span>|
| <span data-ttu-id="513ab-114">[將模擬裝置連線至您的 IoT 中樞][4]</span><span class="sxs-lookup"><span data-stu-id="513ab-114">[Connect a simulated device to your IoT Hub][4]</span></span> | <span data-ttu-id="513ab-115">建立裝置身分識別、傳送訊息，以及處理 IoT 中樞的遙測。</span><span class="sxs-lookup"><span data-stu-id="513ab-115">Create a device identity, send messages, and process telemetry from your IoT Hub.</span></span> |   
| <span data-ttu-id="513ab-116">[處理裝置到雲端的訊息][5]</span><span class="sxs-lookup"><span data-stu-id="513ab-116">[Process device-to-cloud messages][5]</span></span> | <span data-ttu-id="513ab-117">從模擬裝置傳送訊息並在雲端中處理它們。</span><span class="sxs-lookup"><span data-stu-id="513ab-117">Send messages from a simulated device and process them in the cloud.</span></span> |
|<span data-ttu-id="513ab-118">**事件中樞**</span><span class="sxs-lookup"><span data-stu-id="513ab-118">**Event Hub**</span></span>|
| <span data-ttu-id="513ab-119">[將事件傳送到事件中樞][6]</span><span class="sxs-lookup"><span data-stu-id="513ab-119">[Send events to an Event Hub][6]</span></span> | <span data-ttu-id="513ab-120">將事件從主控台應用程式傳送至事件中樞。</span><span class="sxs-lookup"><span data-stu-id="513ab-120">Send events to Event hub from a console application.</span></span>
| <span data-ttu-id="513ab-121">[從事件中樞接收事件][7]</span><span class="sxs-lookup"><span data-stu-id="513ab-121">[Receive events from Event Hubs][7]</span></span> | <span data-ttu-id="513ab-122">接收訊息並以平行方式處理它們。</span><span class="sxs-lookup"><span data-stu-id="513ab-122">Receive messages and process them in parallel.</span></span>


[1]: /azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues
[2]: /azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions
[3]: /azure/service-bus-messaging/service-bus-amqp-dotnet
[4]: /azure/iot-hub/iot-hub-csharp-csharp-getstarted
[5]: /azure/iot-hub/iot-hub-csharp-csharp-process-d2c
[6]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-send
[7]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph


