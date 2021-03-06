---
title: 適用於.NET 的 Azure StorSimple 程式庫
description: 適用於 .NET 的 Azure StorSimple 程式庫參考
ms.date: 10/27/2017
ms.topic: reference
ms.service: storsimple
ms.openlocfilehash: ecaa1acb0d988f7312645c2e6ed8f3289e51237c
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190361"
---
# <a name="azure-storsimple-libraries-for-net"></a>適用於.NET 的 Azure StorSimple 程式庫

## <a name="overview"></a>概觀

Microsoft Azure StorSimple 是企業儲存體解決方案，提供實體 iSCSI 或 SMB 介面及雲端儲存體。 

深入了解 [Azure StorSimple](/azure/storsimple/)。    

## <a name="management-library"></a>管理程式庫

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.StorSimple.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.StorSimple.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.StorSimple.Fluent
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/monitor/management)

## <a name="samples"></a>範例

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package