---
title: "適用於 .NET 的 Azure Data Lake Analytics 程式庫"
description: "適用於 .NET 的 Azure Data Lake Analytics 程式庫參考"
keywords: Azure, .NET, SDK, API, Data Lake Analytics
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/18/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 935afa104b1a47f537ea3bcc981670abd6c56413
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a>適用於 .NET 的 Azure Data Lake Analytics 程式庫

## <a name="overview"></a>概觀

Azure Data Lake Analytics 是隨選分析作業服務，可簡化巨量資料分析。

若要進一步了解，請參閱 [Microsoft Azure Data Lake Analytics 概觀](/azure/data-lake-analytics/data-lake-analytics-overview)。

## <a name="management-library"></a>管理程式庫

使用管理程式庫連線到服務及管理分析作業。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a>程式碼範例

這個範例會建立用戶端以連線及管理分析帳戶。

```csharp
/*
using AdlClient 
*/

// Setup authentication for this demo
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
AnalyticsAccountRef adla_account = new AnalyticsAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
AnalyticsClient adla = new AnalyticsClient(auth, adla_account);
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>範例
* [Azure Data Lake .NET 用戶端範例](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package