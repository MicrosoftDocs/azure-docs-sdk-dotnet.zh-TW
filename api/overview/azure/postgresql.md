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
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="02d91-103">適用於 .NET 的 Azure Database for PostgreSQL 程式庫</span><span class="sxs-lookup"><span data-stu-id="02d91-103">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="02d91-104">概觀</span><span class="sxs-lookup"><span data-stu-id="02d91-104">Overview</span></span>

<span data-ttu-id="02d91-105">使用儲存在 [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/) 的資料和資源。</span><span class="sxs-lookup"><span data-stu-id="02d91-105">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="02d91-106">用戶端 API</span><span class="sxs-lookup"><span data-stu-id="02d91-106">Client API</span></span>

<span data-ttu-id="02d91-107">用於存取 Azure Database for PostgreSQL 的建議用戶端程式庫是開放原始碼的 [Npgsql ADO.NET 資料提供者](http://www.npgsql.org/)。</span><span class="sxs-lookup"><span data-stu-id="02d91-107">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="02d91-108">使用 ADO.NET 提供者以直接連線到資料庫並執行 SQL 陳述式，或透過 Entity Framework 搭配 Npgsql 的 [Entity Framework 6](http://www.npgsql.org/ef6/index.html) 或 [Entity Framework Core](http://www.npgsql.org/efcore/index.html) 提供者。</span><span class="sxs-lookup"><span data-stu-id="02d91-108">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="02d91-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Npgsql)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="02d91-109">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="02d91-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="02d91-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="02d91-111">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="02d91-111">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="02d91-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="02d91-112">Code Example</span></span>

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

### <a name="samples"></a><span data-ttu-id="02d91-113">範例</span><span class="sxs-lookup"><span data-stu-id="02d91-113">Samples</span></span>

- [<span data-ttu-id="02d91-114">ADO.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="02d91-114">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="02d91-115">使用 Azure CLI 設計 PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="02d91-115">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
