---
title: 適用於 .NET 的 Azure 通知中樞程式庫
description: 適用於 .NET 的 Azure 通知中樞程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: notification-hubs
ms.openlocfilehash: 750a51e8dfa7323f6afb54735b4bfc517f9ec15f
ms.sourcegitcommit: 4b68c73652cb7e44cf4db36f70cb33a17dd863ce
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/19/2019
ms.locfileid: "58085835"
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="a59e2-103">適用於 .NET 的 Azure 通知中樞程式庫</span><span class="sxs-lookup"><span data-stu-id="a59e2-103">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="a59e2-104">Azure 通知中樞提供方便使用、多平台、可相應放大的推播引擎。</span><span class="sxs-lookup"><span data-stu-id="a59e2-104">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="a59e2-105">利用單一的跨平台 API 呼叫，您就可以輕鬆地將鎖定目標且個人化的推播通知，從任何雲端或內部部署後端傳送到任何行動平台。</span><span class="sxs-lookup"><span data-stu-id="a59e2-105">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="a59e2-106">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="a59e2-106">Client library</span></span>

<span data-ttu-id="a59e2-107">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="a59e2-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="a59e2-108">[Azure 通知中樞 NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)現在支援 .NET Standard，可允許通知中樞後端使用 .NET 核心</span><span class="sxs-lookup"><span data-stu-id="a59e2-108">The [Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a59e2-109">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="a59e2-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="a59e2-110">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a59e2-110">Code Example</span></span>

<span data-ttu-id="a59e2-111">本範例會連線到通知中樞，並傳送 Windows 推播通知服務 (WNS) 訊息。</span><span class="sxs-lookup"><span data-stu-id="a59e2-111">This example connects to a Notification Hub and sends a Windows Push Notification Service (WNS) message.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a59e2-112">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="a59e2-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)

## <a name="management-library"></a><span data-ttu-id="a59e2-113">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="a59e2-113">Management library</span></span>

<span data-ttu-id="a59e2-114">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="a59e2-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a59e2-115">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="a59e2-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a59e2-116">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="a59e2-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="a59e2-117">範例</span><span class="sxs-lookup"><span data-stu-id="a59e2-117">Samples</span></span>

- [<span data-ttu-id="a59e2-118">Windows Universal 使用者入門</span><span class="sxs-lookup"><span data-stu-id="a59e2-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
