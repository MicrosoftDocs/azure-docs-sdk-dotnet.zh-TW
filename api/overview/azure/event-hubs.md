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
# <a name="azure-event-hubs-libraries-for-net"></a>適用於 .NET 的 Azure 事件中樞程式庫

## <a name="overview"></a>概觀

Azure 事件中樞為可高度擴充的資料串流平台和事件擷取服務。

若要了解有關 Azure 事件中樞的詳細資訊，請參閱文章[何謂事件中樞？](/azure/event-hubs/event-hubs-what-is-event-hubs)。  若要開始使用，請參閱[事件中樞程式設計指南](/azure/event-hubs/event-hubs-programming-guide)。

## <a name="client-library"></a>用戶端程式庫

使用事件中樞用戶端來傳送和接收事件中樞的訊息。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.EventHubs)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a>程式碼範例

下列程式碼會建立事件中樞用戶端，並將訊息傳送至中樞。

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
> [探索用戶端 API](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a>管理程式庫

使用事件中樞管理程式庫來建立、更新及移除中樞和取用者群組。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a>程式碼範例

下列程式碼會建立新的中樞。

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
> [探索管理 API](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a>教學課程

* [使用 .NET Framework 將事件傳送至 Azure 事件中樞](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [使用 .NET Framework 從 Azure 事件中樞接收事件](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a>範例

* [Azure 事件中樞範例](https://github.com/Azure/azure-event-hubs/tree/master/samples)

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
