---
title: 適用於 .NET 的 Azure Database for MySQL 程式庫
description: 適用於 Azure Database for MySQL 之 .NET 用戶端程式庫的參考文件
keywords: Azure, .NET, SDK, API, SQL, 資料庫, MySQL
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: mysql
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 27c1a2c7d36966d14daff5397b248a24197bec3b
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566049"
---
# <a name="azure-database-for-mysql-libraries-for-net"></a>適用於 .NET 的 Azure Database for MySQL 程式庫

## <a name="overview"></a>概觀

使用儲存在 [Azure Database for MySQL](/azure/mysql/overview) 的資料和資源。

## <a name="client-apis"></a>用戶端 API

用於存取 Azure Database for MySQL 的建議用戶端程式庫是 MySQL 的 [Connector/Net](https://dev.mysql.com/doc/connector-net/en)。 使用套件來連線到資料庫並直接執行 SQL 陳述式。 

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/MySql.Data)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a>程式碼範例

連線到 MySQL 資料庫並執行查詢：

```csharp
/* Include this "using" directive...
using MySql.Data.MySqlClient;
*/

string connectionString = "Server=[servername].mysql.database.azure.com; " +
    "Database=myDataBase; Uid=[userid]@[servername]; Pwd=myPassword;";

// Best practice is to scope the MySqlConnection to a "using" block
using (MySqlConnection conn = new MySqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    MySqlCommand selectCommand = new MySqlCommand("SELECT * FROM MyTable", conn);
    MySqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

## <a name="samples"></a>範例

- [ADO.NET 程式碼範例](/dotnet/framework/data/adonet/ado-net-code-examples)
- [使用 Azure CLI 設計 MySQL 資料庫](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
