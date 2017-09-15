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
# <a name="net-tutorials-for-enterprise-messaging-and-internet-of-things-iot"></a>企業傳訊和物聯網 (IoT) 的 .NET 教學課程

下表連線至在 .NET 程式碼中使用 Azure 服務來傳送和讀取應用程式和裝置之間訊息的深入教學課程。

如需範例原始程式碼，請參閱 [Azure 服務範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)清單。


| | |
|---|---|
| **服務匯流排** | |
| [如何使用服務匯流排佇列][1] | 建立佇列、傳送和接收訊息，以及刪除佇列。 | 
| [如何使用服務匯流排主題和訂閱][2] | 了解如何搭配服務匯流排使用發佈/訂閱通訊模型。
| [搭配使用 .NET 的服務匯流排與 AMQP 1.0][3] | 了解如何在您的服務匯流排應用程式中使用 AMQP。
|**IoT 中心**|
| [將模擬裝置連線至您的 IoT 中樞][4] | 建立裝置身分識別、傳送訊息，以及處理 IoT 中樞的遙測。 |   
| [處理裝置到雲端的訊息][5] | 從模擬裝置傳送訊息並在雲端中處理它們。 |
|**事件中樞**|
| [將事件傳送到事件中樞][6] | 將事件從主控台應用程式傳送至事件中樞。
| [從事件中樞接收事件][7] | 接收訊息並以平行方式處理它們。


[1]: /azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues
[2]: /azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions
[3]: /azure/service-bus-messaging/service-bus-amqp-dotnet
[4]: /azure/iot-hub/iot-hub-csharp-csharp-getstarted
[5]: /azure/iot-hub/iot-hub-csharp-csharp-process-d2c
[6]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-send
[7]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph

