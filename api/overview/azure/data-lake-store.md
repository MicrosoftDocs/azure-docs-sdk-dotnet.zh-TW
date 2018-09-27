---
title: 適用於 .NET 的 Azure Data Lake Store 程式庫
description: 適用於 .NET 的 Azure Data Lake Store 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: data-lake-store
ms.openlocfilehash: 8e55a21d84eae2ef4104c8253adec2cbc4b008e5
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190561"
---
# <a name="azure-data-lake-store-libraries-for-net"></a>適用於 .NET 的 Azure Data Lake Store 程式庫

## <a name="overview"></a>概觀

Azure Data Lake Store 是容納巨量資料分析工作負載的企業級超大規模存放庫。 Azure Data Lake 可讓您在單一位置擷取任何大小、類型和擷取速度的資料，以便進行運作和探究分析。

若要進一步了解，請參閱 [Azure Data Lake Store 概觀](/azure/data-lake-store/data-lake-store-overview)。

## <a name="client-library"></a>用戶端程式庫

使用用戶端程式庫在 Data Lake Store 上執行檔案系統作業，例如在 Data Lake Store 帳戶中建立資料夾、上傳及下載檔案。  如果使用 Data Lake Store 搭配 .NET 的完整教學課程，請參閱[在 Azure Data Lake Store 上使用 .NET SDK 的檔案系統作業](/azure/data-lake-store/data-lake-store-data-operations-net-sdk)。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a>驗證

* 如需讓應用程式進行使用者驗證，請參閱[使用 .NET SDK 向 Data Lake Store 進行使用者驗證](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk)。
* 如需讓應用程式進行服務對服務驗證，請參閱[使用 .NET SDK 向 Data Lake Store 進行服務對服務驗證](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk)。

### <a name="code-example"></a>程式碼範例

下列程式碼片段會建立 Data Lake Store 檔案系統用戶端物件，以便對服務發出要求。

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/datalakestore/client)


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

> [!div class="nextstepaction"]
> [探索用戶端 API](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a>範例

* [Azure Data Lake .NET 用戶端範例](https://azure.microsoft.com/resources/samples/data-lake-dotnet-client/)

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
