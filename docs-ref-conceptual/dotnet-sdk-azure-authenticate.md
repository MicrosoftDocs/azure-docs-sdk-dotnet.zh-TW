---
title: "使用適用於 .NET 的 Azure 程式庫來進行驗證"
description: "使用適用於 .NET 的 Azure 程式庫來進行驗證"
keywords: "Azure, .NET, SDK, API, 驗證, Active Directory, 服務主體"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 5bc1f4a576ae3bb38e9d29c890ea79bc0871cd01
ms.sourcegitcommit: fa02d34afbf981f809661ab842b3b93242a38f68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2017
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="5d203-104">使用適用於 .NET 的 Azure 程式庫來進行驗證</span><span class="sxs-lookup"><span data-stu-id="5d203-104">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="5d203-105">使用連接字串來連線到服務</span><span class="sxs-lookup"><span data-stu-id="5d203-105">Connect to services with connection strings</span></span>

<span data-ttu-id="5d203-106">Azure 服務程式庫大多會要求連接字串或金鑰來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="5d203-106">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="5d203-107">例如，SQL Database 會使用標準 SQL 連接字串：</span><span class="sxs-lookup"><span data-stu-id="5d203-107">For example, SQL Database uses a standard SQL connection string:</span></span>

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

<span data-ttu-id="5d203-108">Azure 儲存體會使用儲存體金鑰：</span><span class="sxs-lookup"><span data-stu-id="5d203-108">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="5d203-109">會在其他 Azure 服務中服務連接字串，例如 [CosmosDB](https://docs.microsoft.com/en-us/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db)、[Redis 快取](https://docs.microsoft.com/en-us/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache)和[服務匯流排](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues)，您可以使用 Azure 入口網站、CLI 或PowerShell 來取得這些字串。</span><span class="sxs-lookup"><span data-stu-id="5d203-109">Service connection strings are used in other Azure services like [CosmosDB](https://docs.microsoft.com/en-us/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](https://docs.microsoft.com/en-us/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span>  <span data-ttu-id="5d203-110">您也可以使用適用於 .NET 的 Azure 管理程式庫來查詢資源，從而在程式碼中建置連接字串。</span><span class="sxs-lookup"><span data-stu-id="5d203-110">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="5d203-111">此程式碼片段會使用管理程式庫來建立儲存體帳戶的連接字串：</span><span class="sxs-lookup"><span data-stu-id="5d203-111">This snippet uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="5d203-112">對於其他程式庫，應用程式就必須使用[服務主體](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)來執行，這個服務主體要授權應用程式使用獲授與的認證來執行。</span><span class="sxs-lookup"><span data-stu-id="5d203-112">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="5d203-113">這項設定很類似下面所列管理程式庫中的物件型驗證步驟。</span><span class="sxs-lookup"><span data-stu-id="5d203-113">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <span data-ttu-id="5d203-114"><a name="mgmt-auth"></a>適用於 .NET 驗證的 Azure 管理程式庫</span><span class="sxs-lookup"><span data-stu-id="5d203-114"><a name="mgmt-auth"></a>Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

<span data-ttu-id="5d203-115">現在您已建立服務主體，有兩個選項可用來驗證服務主體，從而建立和管理資源。</span><span class="sxs-lookup"><span data-stu-id="5d203-115">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="5d203-116">針對這兩個選項，您必須將下列 nuget 套件新增至專案。</span><span class="sxs-lookup"><span data-stu-id="5d203-116">For both options you will need to add the following nuget packages to your project.</span></span>

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="5d203-117">使用權杖認證進行驗證</span><span class="sxs-lookup"><span data-stu-id="5d203-117">Authenticate with token credentials</span></span>

<span data-ttu-id="5d203-118">第一個方法是在程式碼中建置權杖認證物件。</span><span class="sxs-lookup"><span data-stu-id="5d203-118">The first method is to build the token credential object in code.</span></span>  <span data-ttu-id="5d203-119">您應該在組態檔、登錄或 Azure Key Vault 中安全地儲存認證。</span><span class="sxs-lookup"><span data-stu-id="5d203-119">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

- <span data-ttu-id="5d203-120">clientId：使用從服務主體輸出所得到的 ApplicationId 值。</span><span class="sxs-lookup"><span data-stu-id="5d203-120">clientId: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="5d203-121">clientSecret：執行 `New-AzureRmADServicePrincipal` 時，使用您指派的 -Password 參數 (不含引號)。</span><span class="sxs-lookup"><span data-stu-id="5d203-121">clientSecret: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="5d203-122">tenantId：執行 `Login-AzureRmAccount` 時，使用 TenantId 值。</span><span class="sxs-lookup"><span data-stu-id="5d203-122">tenantId: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="5d203-123">然後，建立進入點 `Azure` 物件來開始使用 API：</span><span class="sxs-lookup"><span data-stu-id="5d203-123">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <span data-ttu-id="5d203-124"><a name="mgmt-file"></a>以檔案作為基礎的驗證</span><span class="sxs-lookup"><span data-stu-id="5d203-124"><a name="mgmt-file"></a>File-based authentication</span></span>

<span data-ttu-id="5d203-125">以檔案作為基礎的驗證可讓您將服務主體認證放在純文字檔案，並在檔案系統內加以保護。</span><span class="sxs-lookup"><span data-stu-id="5d203-125">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](includes/file-based-auth.md)]

<span data-ttu-id="5d203-126">讀取檔案的內容，並建立進入點 `Azure` 物件來開始使用 API：</span><span class="sxs-lookup"><span data-stu-id="5d203-126">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
