---
title: 適用於 .NET 的 Azure Database for PostgreSQL 程式庫
description: 適用於 Azure Database for PostgreSQL 之 .NET 用戶端程式庫的參考文件
ms.date: 10/19/2017
ms.topic: reference
ms.service: postgresql
ms.openlocfilehash: 4137e024eadba93c9cb3e94c1e7478d0816f8370
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190742"
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a>適用於 .NET 的 Azure Database for PostgreSQL 程式庫

## <a name="overview"></a>概觀

使用儲存在 [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/) 的資料和資源。

## <a name="client-api"></a>用戶端 API

用於存取 Azure Database for PostgreSQL 的建議用戶端程式庫是開放原始碼的 [Npgsql ADO.NET 資料提供者](http://www.npgsql.org/)。 使用 ADO.NET 提供者以直接連線到資料庫並執行 SQL 陳述式，或透過 Entity Framework 搭配 Npgsql 的 [Entity Framework 6](http://www.npgsql.org/ef6/index.html) 或 [Entity Framework Core](http://www.npgsql.org/efcore/index.html) 提供者。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Npgsql)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a>程式碼範例

```csharp
/* Include this 'using' directive...
using Npgsql;
*/

// Always store connection strings securely. 
string connectionString = "Server=[servername].postgres.database.azure.com; " +
    "Port=5432; Database=myDataBase; User Id=[userid]@[servername]; Password=password;";

// Best practice is to scope the NpgsqlConnection to a "using" block
using (NpgsqlConnection conn = new NpgsqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    NpgsqlCommand selectCommand = new NpgsqlCommand("SELECT * FROM MyTable", conn);
    NpgsqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

### <a name="samples"></a>範例

- [ADO.NET 程式碼範例](/dotnet/framework/data/adonet/ado-net-code-examples)
- [使用 Azure CLI 設計 PostgreSQL 資料庫](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
