---
title: 適用於 .NET 的 Azure 通知中樞程式庫
description: 適用於 .NET 的 Azure 通知中樞程式庫參考
keywords: Azure, .NET, SDK, API, 通知中樞
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: notification-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 0cbbfbafd2d1900c00f08fd1ab2e0f1af80ae8ff
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065498"
---
# <a name="azure-notification-hubs-libraries-for-net"></a>適用於 .NET 的 Azure 通知中樞程式庫

Azure 通知中樞提供方便使用、多平台、可相應放大的推播引擎。 利用單一的跨平台 API 呼叫，您就可以輕鬆地將鎖定目標且個人化的推播通知，從任何雲端或內部部署後端傳送到任何行動平台。

## <a name="client-library"></a>用戶端程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。

> [!NOTE]
> [全新的 NuGet 套件預覽版本](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/2.0.0-preview1)現可支援 .NET Standard，可讓通知中樞後端使用 .NET 核心

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a>程式碼範例

本範例會連線到通知中樞，並傳送 Windows 推播通知服務 (WNS) 訊息。

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a>管理程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a>範例

- [Windows Universal 使用者入門](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
