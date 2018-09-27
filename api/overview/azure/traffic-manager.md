---
title: 適用於 .NET 的 Azure 流量管理員程式庫
description: 適用於 .NET 的 Azure 流量管理員程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: traffic-manager
ms.openlocfilehash: a75b5c566496f73475d24d62288a00c7d5775168
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190813"
---
# <a name="azure-traffic-manager-libraries-for-net"></a>適用於 .NET 的 Azure 流量管理員程式庫

## <a name="overview"></a>概觀

Microsoft Azure 流量管理員可讓您控制使用者流量，將流量分散到不同資料中心的服務端點。 流量管理員支援的服務端點包括 Azure VM、Web Apps 和雲端服務。 您也可以將流量管理員使用於外部、非 Azure 端點。

深入了解 [Azure 流量管理員](/azure/traffic-manager/traffic-manager-overview)。  

## <a name="management-library"></a>管理程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a>範例

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package