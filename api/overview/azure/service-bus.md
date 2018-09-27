---
title: 適用於 .NET 的 Azure 服務匯流排程式庫
description: 適用於 .NET 的 Azure 服務匯流排程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus
ms.openlocfilehash: 506be9a669a2418f2437271d128a963e351442e7
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190871"
---
# <a name="azure-service-bus-libraries-for-net"></a>適用於 .NET 的 Azure 服務匯流排程式庫

## <a name="overview"></a>概觀

[Azure 服務匯流排](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview)是座落在應用程式之間的訊息基礎結構，可讓應用程式交換訊息以增進規模和恢復功能。

## <a name="client-library"></a>用戶端程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus)。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a>程式碼範例

這個範例會將訊息傳送至服務匯流排佇列。

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a>管理程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a>程式碼範例

這個範例會建立服務匯流排佇列，大小上限為 1024 MB。

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
> [探索管理 API](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a>範例

- [服務匯流排基本 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [服務匯流排進階功能 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [服務匯流排發佈/訂閱基本 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [服務匯流排發佈/訂閱進階功能 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [具宣告式授權的服務匯流排 - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

檢視 Azure 服務匯流排範例的[完整清單](https://azure.microsoft.com/resources/samples/?term=service+bus)。


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
