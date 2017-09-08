---
title: "適用於 .NET 的 Azure Database for MySQL 程式庫"
description: "適用於 Azure Database for MySQL 之 .NET 用戶端程式庫的參考文件"
keywords: "Azure, .NET, SDK, API, SQL, 資料庫, MySQL"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: mysql
ms.openlocfilehash: 1bc373d63b0172fd554277a6ef30fa09772a395b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-mysql-libraries-for-net"></a><span data-ttu-id="f4a13-104">適用於 .NET 的 Azure Database for MySQL 程式庫</span><span class="sxs-lookup"><span data-stu-id="f4a13-104">Azure Database for MySQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="f4a13-105">概觀</span><span class="sxs-lookup"><span data-stu-id="f4a13-105">Overview</span></span>

<span data-ttu-id="f4a13-106">使用儲存在 [Azure Database for MySQL](/azure/mysql/overview) 的資料和資源。</span><span class="sxs-lookup"><span data-stu-id="f4a13-106">Work with data and resources stored in [Azure Database for MySQL](/azure/mysql/overview).</span></span>

## <a name="client-apis"></a><span data-ttu-id="f4a13-107">用戶端 API</span><span class="sxs-lookup"><span data-stu-id="f4a13-107">Client APIs</span></span>

<span data-ttu-id="f4a13-108">用於存取 Azure Database for MySQL 的建議用戶端程式庫是 MySQL 的 [Connector/Net](https://dev.mysql.com/doc/connector-net/en)。</span><span class="sxs-lookup"><span data-stu-id="f4a13-108">The recommended client library for accessing Azure Database for MySQL is MySQL's [Connector/Net](https://dev.mysql.com/doc/connector-net/en).</span></span> <span data-ttu-id="f4a13-109">使用套件來連線到資料庫並直接執行 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="f4a13-109">Use the package to connect to the database and execute SQL statements directly.</span></span> 

<span data-ttu-id="f4a13-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/MySql.Data)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="f4a13-110">Install the [NuGet package](https://www.nuget.org/packages/MySql.Data) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f4a13-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="f4a13-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a><span data-ttu-id="f4a13-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="f4a13-112">.NET Core CLI</span></span>

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a><span data-ttu-id="f4a13-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="f4a13-113">Code Example</span></span>

<span data-ttu-id="f4a13-114">連線到 MySQL 資料庫並執行查詢：</span><span class="sxs-lookup"><span data-stu-id="f4a13-114">Connect to a MySQL database and execute a query:</span></span>

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

## <a name="samples"></a><span data-ttu-id="f4a13-115">範例</span><span class="sxs-lookup"><span data-stu-id="f4a13-115">Samples</span></span>

- [<span data-ttu-id="f4a13-116">ADO.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="f4a13-116">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="f4a13-117">使用 Azure CLI 設計 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="f4a13-117">Design a MySQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
