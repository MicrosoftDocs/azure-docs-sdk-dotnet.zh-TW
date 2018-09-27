---
title: 使用適用於 .NET 的 Azure 程式庫來進行驗證
description: 使用適用於 .NET 的 Azure 程式庫來進行驗證
ms.date: 08/22/2018
ms.openlocfilehash: d0d8db89816a887fa23490a213917a3c554ecdb4
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190857"
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="0a0e2-103">使用適用於 .NET 的 Azure 程式庫來進行驗證</span><span class="sxs-lookup"><span data-stu-id="0a0e2-103">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="0a0e2-104">使用連接字串來連線到服務</span><span class="sxs-lookup"><span data-stu-id="0a0e2-104">Connect to services with connection strings</span></span>

<span data-ttu-id="0a0e2-105">Azure 服務程式庫大多會要求連接字串或金鑰來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-105">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="0a0e2-106">例如，SQL Database 會使用標準 SQL 連接字串：</span><span class="sxs-lookup"><span data-stu-id="0a0e2-106">For example, SQL Database uses a standard SQL connection string:</span></span>

```csharp
var builder = new SqlConnectionStringBuilder();
builder.DataSource = "example.database.windows.net";
builder.InitialCatalog = "MyDatabase";
builder.UserID = "sampleuser@example"; // Format user ID as "user@server"
builder.Password = password;
builder.Encrypt = true;
builder.TrustServerCertificate = true;
                
using (var conn = new SqlConnection(builder.ConnectionString))
{
    conn.Open();
    // Do things with the connection...
    // ...
}
```

<span data-ttu-id="0a0e2-107">Azure 儲存體會使用儲存體金鑰：</span><span class="sxs-lookup"><span data-stu-id="0a0e2-107">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="0a0e2-108">會在其他 Azure 服務中服務連接字串，例如 [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db)、[Redis 快取](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache)和[服務匯流排](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues)，您可以使用 Azure 入口網站、CLI 或PowerShell 來取得這些字串。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-108">Service connection strings are used in other Azure services like [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span>  <span data-ttu-id="0a0e2-109">您也可以使用適用於 .NET 的 Azure 管理程式庫來查詢資源，從而在程式碼中建置連接字串。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-109">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="0a0e2-110">此程式碼片段會使用管理程式庫來建立儲存體帳戶的連接字串：</span><span class="sxs-lookup"><span data-stu-id="0a0e2-110">This snippet uses the management libraries to create a storage account connection string:</span></span>

```csharp
// Get a storage account
var storage = azure.StorageAccounts.GetByResourceGroup("myResourceGroup", "myStorageAccount");

// Extract the keys
var storageKeys = storage.GetKeys();

// Build the connection string
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

// Connect
var account = CloudStorageAccount.Parse(storageConnectionString);

// Do things with the account here...
```

<span data-ttu-id="0a0e2-111">對於其他程式庫，應用程式就必須使用[服務主體](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)來執行，這個服務主體要授權應用程式使用獲授與的認證來執行。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-111">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="0a0e2-112">這項設定很類似下面所列管理程式庫中的物件型驗證步驟。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-112">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <a name="mgmt-auth"></a><span data-ttu-id="0a0e2-113">適用於 .NET 驗證的 Azure 管理程式庫</span><span class="sxs-lookup"><span data-stu-id="0a0e2-113">Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

<span data-ttu-id="0a0e2-114">現在您已建立服務主體，有兩個選項可用來驗證服務主體，從而建立和管理資源。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-114">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="0a0e2-115">針對這兩個選項，您必須將下列 nuget 套件新增至專案。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-115">For both options you will need to add the following nuget packages to your project.</span></span>

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="0a0e2-116">使用權杖認證進行驗證</span><span class="sxs-lookup"><span data-stu-id="0a0e2-116">Authenticate with token credentials</span></span>

<span data-ttu-id="0a0e2-117">第一個方法是在程式碼中建置權杖認證物件。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-117">The first method is to build the token credential object in code.</span></span>  <span data-ttu-id="0a0e2-118">您應該在組態檔、登錄或 Azure Key Vault 中安全地儲存認證。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-118">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

<span data-ttu-id="0a0e2-119">使用 *clientId*、*clientSecret*和 *tenantId* 等值，這些值來自已建立服務主體處的 JSON 輸出。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-119">Use the *clientId*, *clientSecret*, and *tenantId* values from the JSON output when you created the service principal.</span></span>

<span data-ttu-id="0a0e2-120">然後，建立進入點 `Azure` 物件來開始使用 API：</span><span class="sxs-lookup"><span data-stu-id="0a0e2-120">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="mgmt-file"></a><span data-ttu-id="0a0e2-121">以檔案作為基礎的驗證</span><span class="sxs-lookup"><span data-stu-id="0a0e2-121">File-based authentication</span></span>

<span data-ttu-id="0a0e2-122">以檔案作為基礎的驗證可讓您將服務主體認證放在純文字檔案，並在檔案系統內加以保護。</span><span class="sxs-lookup"><span data-stu-id="0a0e2-122">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](includes/file-based-auth.md)]

<span data-ttu-id="0a0e2-123">讀取檔案的內容，並建立進入點 `Azure` 物件來開始使用 API：</span><span class="sxs-lookup"><span data-stu-id="0a0e2-123">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
