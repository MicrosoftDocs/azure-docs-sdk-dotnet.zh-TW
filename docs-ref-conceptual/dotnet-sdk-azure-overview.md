---
title: Azure .NET API
description: 適用於 .NET 的 Azure API 概觀
keywords: Azure, .NET, SDK, API, NuGet, 程式庫, 套件
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 26360a516220ca9d3e8901e60cb23ecbd02863cd
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752690"
---
# <a name="azure-net-apis"></a>Azure .NET API

Azure .NET API 可讓您使用 Azure 服務，並從應用程式程式碼管理 Azure 資源。 API 可作為 [NuGet 套件](/dotnet/api/overview/azure/)，在 .NET 專案中使用。 

## <a name="manage-azure-resources"></a>管理 Azure 資源

適用於 .NET 的 Azure 程式庫可讓您從 .NET 應用程式建立並管理 Azure 資源。

許多管理 Azure 資源的套件都有 [Fluent](dotnet-sdk-azure-concepts.md) 介面，可完全以您的規格設定資源。 例如，若要建立 Windows VM，您需要撰寫下列程式碼：

```csharp
var windowsVM = azure.VirtualMachines.Define(windowsVmName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername(username)
    .WithAdminPassword(password)
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
 ```

檢閱 [.NET 服務清單](/dotnet/api/overview/azure/)，立即開始使用程式庫與您的專案。 然後讀取[開始使用文章](dotnet-sdk-azure-get-started.md)，針對您自己的 Azure 訂用帳戶設定驗證並執行範例程式碼。  [概念文件](dotnet-sdk-azure-concepts.md)會討論 SDK 所使用的慣例，以及如何利用它們來簡化您的應用程式程式碼。 新功能、重大變更以及移轉的指示則會在[版本資訊](dotnet-sdk-azure-release-notes.md)中提供。

## <a name="consume-azure-services"></a>取用 Azure 服務

除了可以使用 .NET API 來建立 Azure 內的資源並以程式設計方式加以管理，您也可以使用 .NET API 將應用程式連線到這些資源，並在執行階段使用它們。  例如，您可以連線到 SQL Database，或在 Azure 儲存體內儲存資料。  您可以瀏覽[服務 API 的完整清單](/dotnet/api/overview/azure/)，來識別要用於特定 Azure 服務的 NuGet 套件。  

## <a name="samples"></a>範例

下列範例涵蓋常見的自動化工作，並包含適用於 .NET 的 Azure 程式庫：

- [虛擬機器](dotnet-sdk-azure-virtual-machine-samples.md)
- [Web Apps](dotnet-sdk-azure-web-apps-samples.md)
- [SQL Database](dotnet-sdk-azure-sql-database-samples.md)

我們提供了一個適用於服務和管理程式庫中所有套件的統一[參考](/dotnet/api/overview/azure/?view=azure-dotnet)。 新功能、重大變更以及移轉的指示則會在[版本資訊](dotnet-sdk-azure-release-notes.md)中提供。

[!include[Contribute and community](includes/contribute.md)]