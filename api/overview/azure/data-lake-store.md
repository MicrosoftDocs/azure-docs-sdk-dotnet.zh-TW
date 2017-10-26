---
title: "適用於 .NET 的 Azure Data Lake Store 程式庫"
description: "適用於 .NET 的 Azure Data Lake Store 程式庫參考"
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2b1c51575872b12a94eb44c7c082996bb879bcc9
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a>適用於 .NET 的 Azure Data Lake Store 程式庫

## <a name="overview"></a>概觀

Azure Data Lake Store 是容納巨量資料分析工作負載的企業級超大規模存放庫。 Azure Data Lake 可讓您在單一位置擷取任何大小、類型和擷取速度的資料，以便進行運作和探究分析。

若要進一步了解，請參閱 [Azure Data Lake Store 概觀](/azure/data-lake-store/data-lake-store-overview)。

## <a name="management-library"></a>管理程式庫

使用管理程式庫來連線並管理您的巨量資料存放庫。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a>程式碼範例

此範例會向分析帳戶和存放區進行驗證，並建立管理所需的用戶端。

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [探索管理 API](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a>範例

* [Azure Data Lake .NET 用戶端範例](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
