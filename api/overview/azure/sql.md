---
title: 適用於 .NET 的 Azure SQL Database API
description: 適用於 .NET 的 Azure SQL Database 程式庫參考
keywords: Azure, .NET, SDK, API, SQL, SQL Database
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: sql-database
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 3aba3c77935e0f00c7396b4cafa06be32ae2a50d
ms.sourcegitcommit: c360a22d5bff6eedd714b28b847d2f26b06665f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2017
ms.locfileid: "24533103"
---
# <a name="azure-sql-database-apis-for-net"></a><span data-ttu-id="fdc7c-104">適用於 .NET 的 Azure SQL Database API</span><span class="sxs-lookup"><span data-stu-id="fdc7c-104">Azure SQL Database APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="fdc7c-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fdc7c-105">Overview</span></span>

<span data-ttu-id="fdc7c-106">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) 是使用 Microsoft SQL Server 引擎的資料庫服務，可支援關聯式、JSON、空間和 XML 資料。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-106">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) is a database service using the Microsoft SQL Server engine that supports relational, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="fdc7c-107">若要深入了解如何使用 SQL Database 搭配 .NET，請參閱[使用 .NET 搭配 Visual Studio 來連線及查詢 Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-107">To learn more about the using SQL Database with .NET, see [Use .NET with Visual Studio to connect and query an Azure SQL database](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span></span>

## <a name="client-library"></a><span data-ttu-id="fdc7c-108">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="fdc7c-108">Client library</span></span>

<span data-ttu-id="fdc7c-109">使用 .NET SQL 用戶端程式庫來連線及驗證您的資料庫，並執行特定 T-SQL 陳述式和預存程序。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-109">Use the .NET SQL client library to connect and authenticate with your database and execute ad-hoc T-SQL statements and stored procedures.</span></span>

<span data-ttu-id="fdc7c-110">直接從 Visual Studio [套件管理員主控台](https://docs.microsoft.com/nuget/tools/package-manager-console) 安裝 [NuGet 套件]( https://www.nuget.org/packages/System.Data.SqlClient) ，或使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package)。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-110">Install the [NuGet package]( https://www.nuget.org/packages/System.Data.SqlClient) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fdc7c-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="fdc7c-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a><span data-ttu-id="fdc7c-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="fdc7c-112">.NET Core CLI</span></span>

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a><span data-ttu-id="fdc7c-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="fdc7c-113">Code Example</span></span>

<span data-ttu-id="fdc7c-114">這個範例會連線到資料庫，並從資料表讀取資料列。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-114">This example connects to a database and reads rows from a table.</span></span>

```csharp
/* Include this 'using' directive...
using System.Data.SqlClient;
*/

// Always store connection strings securely. 
string connectionString = "Server=tcp:[serverName].database.windows.net;" 
    + "Database=myDataBase;User ID=[loginname]@[serverName];Password=myPassword;"
    + "Trusted_Connection=False;Encrypt=True;";

// Best practice is to scope the SqlConnection to a "using" block
using (SqlConnection conn = new SqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    SqlCommand selectCommand = new SqlCommand("SELECT * FROM MyTable", conn);
    SqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdc7c-115">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="fdc7c-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a><span data-ttu-id="fdc7c-116">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="fdc7c-116">Management library</span></span>

<span data-ttu-id="fdc7c-117">您可以使用 Azure SQL Database 管理程式庫來建立、管理及擴充 Azure SQL Database 伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-117">Use the Azure SQL Database management library to create, manage, and scale Azure SQL Database server instances.</span></span>

<span data-ttu-id="fdc7c-118">直接從 Visual Studio [套件管理員主控台](https://docs.microsoft.com/nuget/tools/package-manager-console) 安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) ，或使用 [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package)。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fdc7c-119">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="fdc7c-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a><span data-ttu-id="fdc7c-120">.NET Core 命令列</span><span class="sxs-lookup"><span data-stu-id="fdc7c-120">.NET Core command line</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a><span data-ttu-id="fdc7c-121">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="fdc7c-121">Code Example</span></span>

<span data-ttu-id="fdc7c-122">此範例會建立新的 SQL Database 伺服器執行個體，然後在該執行個體上建立新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-122">This example creates a new SQL Database server instance and then creates a new database on that instance.</span></span>

```csharp
/* Include these 'using' directives...
using Microsoft.Azure.Management.Sql.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

string startAddress = "0.0.0.0";
string endAddress = "255.255.255.255";

// Create the SQL server instance
ISqlServer sqlServer = azure.SqlServers.Define("UniqueServerName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("ResourceGroupName")
    .WithAdministratorLogin("UserName")
    .WithAdministratorPassword("Password")
    .WithNewFirewallRule(startAddress, endAddress)
    .Create();

// Create the database
ISqlDatabase sqlDb = sqlServer.Databases.Define("DatabaseName").Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdc7c-123">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="fdc7c-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a><span data-ttu-id="fdc7c-124">範例</span><span class="sxs-lookup"><span data-stu-id="fdc7c-124">Samples</span></span>

- [<span data-ttu-id="fdc7c-125">ADO.NET 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="fdc7c-125">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="fdc7c-126">針對 SQL 資料庫所提供之適用於 .NET 的 Azure 管理程式庫範例</span><span class="sxs-lookup"><span data-stu-id="fdc7c-126">Azure management libraries for .NET samples for SQL Database</span></span>](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

<span data-ttu-id="fdc7c-127">檢視 Azure SQL Database 範例的[完整清單](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=sql+database)。</span><span class="sxs-lookup"><span data-stu-id="fdc7c-127">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=sql+database) of Azure SQL Database samples.</span></span>

