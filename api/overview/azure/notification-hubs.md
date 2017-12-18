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
ms.openlocfilehash: 9fd49ccc8d02eff09a8a53e6f1b9baa6a7a59082
ms.sourcegitcommit: 33732307162ddf6f272b0e9cc7f74eb8e6fdda1b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/12/2017
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="da4fb-104">適用於 .NET 的 Azure 通知中樞程式庫</span><span class="sxs-lookup"><span data-stu-id="da4fb-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="da4fb-105">Azure 通知中樞提供方便使用、多平台、可相應放大的推播引擎。</span><span class="sxs-lookup"><span data-stu-id="da4fb-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="da4fb-106">利用單一的跨平台 API 呼叫，您就可以輕鬆地將鎖定目標且個人化的推播通知，從任何雲端或內部部署後端傳送到任何行動平台。</span><span class="sxs-lookup"><span data-stu-id="da4fb-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="da4fb-107">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="da4fb-107">Client library</span></span>

<span data-ttu-id="da4fb-108">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="da4fb-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="da4fb-109">[全新的 NuGet 套件預覽版本](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1)現可支援 .NET Standard，可讓通知中樞後端使用 .NET 核心</span><span class="sxs-lookup"><span data-stu-id="da4fb-109">A [new preview version of the NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="da4fb-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="da4fb-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="da4fb-111">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="da4fb-111">Code Example</span></span>

<span data-ttu-id="da4fb-112">這個範例會連線到資料庫，並從資料表讀取資料列。</span><span class="sxs-lookup"><span data-stu-id="da4fb-112">This example connects to a database and reads rows from a table.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="da4fb-113">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="da4fb-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="da4fb-114">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="da4fb-114">Management library</span></span>

<span data-ttu-id="da4fb-115">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="da4fb-115">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="da4fb-116">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="da4fb-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="da4fb-117">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="da4fb-117">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="da4fb-118">範例</span><span class="sxs-lookup"><span data-stu-id="da4fb-118">Samples</span></span>

- [<span data-ttu-id="da4fb-119">Windows Universal 使用者入門</span><span class="sxs-lookup"><span data-stu-id="da4fb-119">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
