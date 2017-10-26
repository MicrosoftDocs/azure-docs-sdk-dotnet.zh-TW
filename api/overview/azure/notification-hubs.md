---
title: "適用於 .NET 的 Azure 通知中樞程式庫"
description: "適用於 .NET 的 Azure 通知中樞程式庫參考"
keywords: "Azure, .NET, SDK, API, 通知中樞"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: notification-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 6fe4e3f25aa420322478dc7c10aecd055a70f5c8
ms.sourcegitcommit: 4114b8821f20e02f4185fcea7549d716f29b9c90
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/24/2017
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="5f82a-104">適用於 .NET 的 Azure 通知中樞程式庫</span><span class="sxs-lookup"><span data-stu-id="5f82a-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="5f82a-105">Azure 通知中樞提供方便使用、多平台、可相應放大的推播引擎。</span><span class="sxs-lookup"><span data-stu-id="5f82a-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="5f82a-106">利用單一的跨平台 API 呼叫，您就可以輕鬆地將鎖定目標且個人化的推播通知，從任何雲端或內部部署後端傳送到任何行動平台。</span><span class="sxs-lookup"><span data-stu-id="5f82a-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="5f82a-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="5f82a-107">Client library</span></span>

<span data-ttu-id="5f82a-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="5f82a-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5f82a-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="5f82a-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="5f82a-110">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="5f82a-110">Code Example</span></span>

<span data-ttu-id="5f82a-111">這個範例會連線到資料庫，並從資料表讀取資料列。</span><span class="sxs-lookup"><span data-stu-id="5f82a-111">This example connects to a database and reads rows from a table.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f82a-112">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="5f82a-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="5f82a-113">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="5f82a-113">Management library</span></span>

<span data-ttu-id="5f82a-114">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="5f82a-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5f82a-115">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="5f82a-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f82a-116">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="5f82a-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="5f82a-117">範例</span><span class="sxs-lookup"><span data-stu-id="5f82a-117">Samples</span></span>

- [<span data-ttu-id="5f82a-118">Windows Universal 使用者入門</span><span class="sxs-lookup"><span data-stu-id="5f82a-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
