---
title: "適用於.NET 的 Azure StorSimple 程式庫"
description: "適用於 .NET 的 Azure StorSimple 程式庫參考"
keywords: Azure, .NET, SDK, API, StorSimple
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/27/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: storsimple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: dcb6732bf1eded6852a3185546a09c96cfe84eca
ms.sourcegitcommit: 64c9e16e42894e8db8ed088487e55c5e0edd6861
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2017
---
# <a name="azure-storsimple-libraries-for-net"></a><span data-ttu-id="0b401-104">適用於.NET 的 Azure StorSimple 程式庫</span><span class="sxs-lookup"><span data-stu-id="0b401-104">Azure StorSimple libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0b401-105">概觀</span><span class="sxs-lookup"><span data-stu-id="0b401-105">Overview</span></span>

<span data-ttu-id="0b401-106">Microsoft Azure StorSimple 是企業儲存體解決方案，提供實體 iSCSI 或 SMB 介面及雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="0b401-106">Microsoft Azure StorSimple is an enterprise storage solution that provides physical iSCSI or SMB interfaces to cloud-based storage.</span></span> 

<span data-ttu-id="0b401-107">深入了解 [Azure StorSimple](/azure/storsimple/)。</span><span class="sxs-lookup"><span data-stu-id="0b401-107">Learn more about [Azure StorSimple](/azure/storsimple/).</span></span>    

## <a name="management-library"></a><span data-ttu-id="0b401-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="0b401-108">Management library</span></span>

<span data-ttu-id="0b401-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.StorSimple.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="0b401-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StorSimple.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0b401-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="0b401-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StorSimple.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.StorSimple.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0b401-111">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="0b401-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/monitor/management)

## <a name="samples"></a><span data-ttu-id="0b401-112">範例</span><span class="sxs-lookup"><span data-stu-id="0b401-112">Samples</span></span>

<span data-ttu-id="0b401-113">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="0b401-113">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package