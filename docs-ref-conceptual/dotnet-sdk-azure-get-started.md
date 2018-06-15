---
title: 開始使用 Azure .NET API
description: 使用自有 Azure 訂用帳戶開始進行適用於 .NET 之 Azure 程式庫的基本使用。
keywords: Azure, .NET, SDK, API , 驗證, 開始使用
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a3733898f948dbb2ec07da20aa61724e07f23e73
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752870"
---
# <a name="get-started-with-the-azure-net-apis"></a><span data-ttu-id="5e60b-104">開始使用適用於 .NET 的 Azure SDK</span><span class="sxs-lookup"><span data-stu-id="5e60b-104">Get started with the Azure .NET APIs</span></span>

<span data-ttu-id="5e60b-105">本教學課程會示範數個[適用於 .NET 的 Azure API](/dotnet/api/overview/azure/)使用方式。</span><span class="sxs-lookup"><span data-stu-id="5e60b-105">This tutorial demonstrates the usage of several [Azure APIs for .NET](/dotnet/api/overview/azure/).</span></span>  <span data-ttu-id="5e60b-106">您將設定驗證、建立和使用 Azure 儲存體帳戶、建立和使用 Azure SQL Database、部署部分的虛擬機器，以及從 GitHub 部署 Azure App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e60b-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e60b-107">先決條件</span><span class="sxs-lookup"><span data-stu-id="5e60b-107">Prerequisites</span></span>

- <span data-ttu-id="5e60b-108">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5e60b-108">An Azure account.</span></span> <span data-ttu-id="5e60b-109">如果您沒有帳戶，請[取得免費試用帳戶](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="5e60b-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- [<span data-ttu-id="5e60b-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e60b-110">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

## <a name="set-up-authentication"></a><span data-ttu-id="5e60b-111">設定驗證</span><span class="sxs-lookup"><span data-stu-id="5e60b-111">Set up authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a><span data-ttu-id="5e60b-112">建立新專案</span><span class="sxs-lookup"><span data-stu-id="5e60b-112">Create a new project</span></span> 

<span data-ttu-id="5e60b-113">這會建立新的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="5e60b-113">Create a new console application project.</span></span>  <span data-ttu-id="5e60b-114">在 Visual Studio 中，按一下 [檔案]、[新增]，然後按一下 [專案...] 來這麼做。在 Visual C# 範本下，選取 [主控台應用程式 (.NET Core)]、命名您的專案，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="5e60b-114">In Visual Studio, do this by clicking **File**, **New**, and then clicking **Project...**.  Under the Visual C# templates, select **Console App (.NET Core)**, name your project, and then click **OK**.</span></span>

![[新增專案] 對話方塊](media/dotnet-sdk-azure-get-started/new-project.png)

<span data-ttu-id="5e60b-116">建立新的主控台應用程式時，可開啟「套件管理員主控台」，方法是按一下 [工具]、[NuGet 套件管理員]，然後按一下 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="5e60b-116">When the new console app is created, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>  <span data-ttu-id="5e60b-117">在主控台中，可執行下列三個命令來取得您需要的套件：</span><span class="sxs-lookup"><span data-stu-id="5e60b-117">In the console, get the packages you'll need by executing the following three commands:</span></span>

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a><span data-ttu-id="5e60b-118">指示詞</span><span class="sxs-lookup"><span data-stu-id="5e60b-118">Directives</span></span>

<span data-ttu-id="5e60b-119">編輯應用程式的 `Program.cs` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5e60b-119">Edit your application's `Program.cs` file.</span></span>  <span data-ttu-id="5e60b-120">使用下列內容取代頂端的 `using` 指示詞：</span><span class="sxs-lookup"><span data-stu-id="5e60b-120">Replace the `using` directives at the top with the following:</span></span>

```csharp
using System;
using System.Linq;
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Data.SqlClient;
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="5e60b-121">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5e60b-121">Create a virtual machine</span></span>

<span data-ttu-id="5e60b-122">此範例會部署虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5e60b-122">This example deploys a virtual machine.</span></span> 

<span data-ttu-id="5e60b-123">使用下列項目來取代 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="5e60b-123">Replace the `Main` method with the following.</span></span>  <span data-ttu-id="5e60b-124">務必提供虛擬機器的實際 `username` 和 `password`。</span><span class="sxs-lookup"><span data-stu-id="5e60b-124">Be sure to provide an actual `username` and `password` for the virtual machine.</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP";

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the VM
    Console.WriteLine("Creating VM...");
    var windowsVM = azure.VirtualMachines.Define(windowsVmName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewPrimaryNetwork("10.0.0.0/28")
        .WithPrimaryPrivateIPAddressDynamic()
        .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
        .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
        .WithAdminUsername(username)
        .WithAdminPassword(password)
        .WithSize(VirtualMachineSizeTypes.StandardD2V2)
        .Create();

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="5e60b-125">按 **F5** 以執行範例。</span><span class="sxs-lookup"><span data-stu-id="5e60b-125">Press **F5** to run the sample.</span></span>

<span data-ttu-id="5e60b-126">幾分鐘之後，程式就會完成，提示您按下輸入。</span><span class="sxs-lookup"><span data-stu-id="5e60b-126">After several minutes, the program will finish, prompting you to press enter.</span></span> <span data-ttu-id="5e60b-127">按下輸入後，使用 PowerShell 來確認您訂用帳戶中的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="5e60b-127">After pressing enter, verify the virtual machine in your subscription with PowerShell:</span></span>

```powershell
Get-AzureRmVm -ResourceGroupName sampleResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="5e60b-128">從 GitHub 存放庫部署 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5e60b-128">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="5e60b-129">現在，您將修改程式碼，從現有的 GitHub 存放庫建立部署新的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5e60b-129">Now you'll modify your code to create a deploy a new web app from an existing GitHub repository.</span></span> <span data-ttu-id="5e60b-130">以下列程式碼取代 `Main` 方法：</span><span class="sxs-lookup"><span data-stu-id="5e60b-130">Replace the `Main` method with the following code:</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string appName = SdkContext.RandomResourceName("WebApp", 20);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the web app
    Console.WriteLine("Creating Web App...");
    var app = azure.WebApps.Define(appName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewFreeAppServicePlan()
        .DefineSourceControl()
        .WithPublicGitRepository("https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
        .WithBranch("master")
        .Attach()
        .Create();
    Console.WriteLine("Your web app is live at: https://{0}", app.HostNames.First());

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

<span data-ttu-id="5e60b-131">如過去一樣，按下 **F5** 來執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="5e60b-131">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="5e60b-132">開啟瀏覽器並瀏覽至主控台中顯示的 URL，即可驗證部署。</span><span class="sxs-lookup"><span data-stu-id="5e60b-132">Verify the deployment by opening a browser and navigating to URL displayed in the console.</span></span>

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="5e60b-133">連線到 SQL Database</span><span class="sxs-lookup"><span data-stu-id="5e60b-133">Connect to a SQL database</span></span>

<span data-ttu-id="5e60b-134">此範例會建立新的 Azure SQL Database，並執行一些 SQL 作業。</span><span class="sxs-lookup"><span data-stu-id="5e60b-134">This example creates a new Azure SQL Database and performs a few SQL operations.</span></span>

<span data-ttu-id="5e60b-135">使用下列項目取代 `Main` 方法，並確認指派 `dbPassword` 的強式密碼：</span><span class="sxs-lookup"><span data-stu-id="5e60b-135">Replace the `Main` method with the following, making sure to assign a strong password for `dbPassword`:</span></span>

```csharp
 static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string adminUser = SdkContext.RandomResourceName("db", 8);
    string sqlServerName = SdkContext.RandomResourceName("sql", 10);
    string sqlDbName = SdkContext.RandomResourceName("dbname", 8);
    string dbPassword = "YOUR_PASSWORD_HERE";

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the SQL server and database
    Console.WriteLine("Creating server...");
    var sqlServer = azure.SqlServers.Define(sqlServerName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithAdministratorLogin(adminUser)
        .WithAdministratorPassword(dbPassword)
        .WithNewFirewallRule("0.0.0.0", "255.255.255.255")
        .Create();

    Console.WriteLine("Creating database...");
    var sqlDb = sqlServer.Databases.Define(sqlDbName).Create();
    
    // Display information for connecting later...
    Console.WriteLine("Created database {0} in server {1}.", sqlDbName, sqlServer.FullyQualifiedDomainName);
    Console.WriteLine("Your user name is {0}.", adminUser + "@" + sqlServer.Name);
    
    // Build the connection string
    var builder = new SqlConnectionStringBuilder();
    builder.DataSource = sqlServer.FullyQualifiedDomainName;
    builder.InitialCatalog = sqlDbName;
    builder.UserID = adminUser + "@" + sqlServer.Name; // Format user ID as "user@server"
    builder.Password = dbPassword;
    builder.Encrypt = true;
    builder.TrustServerCertificate = true;

    // connect to the database, create a table and insert an entry into it
    using (var conn = new SqlConnection(builder.ConnectionString))
    {
        conn.Open();

        Console.WriteLine("Populating database...");
        var createCommand = new SqlCommand("CREATE TABLE CLOUD (name varchar(255), code int);", conn);
        createCommand.ExecuteNonQuery();

        var insertCommand = new SqlCommand("INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);", conn);
        insertCommand.ExecuteNonQuery();

        Console.WriteLine("Reading from database...");
        var selectCommand = new SqlCommand("SELECT * FROM CLOUD", conn);
        var results = selectCommand.ExecuteReader();
        while(results.Read())
        {
            Console.WriteLine("Name: {0} Code: {1}", results[0], results[1]);
        }
    }

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```
<span data-ttu-id="5e60b-136">如過去一樣，按下 **F5** 來執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="5e60b-136">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="5e60b-137">主控台輸出應該要驗證伺服器已建立並如預期運作，但您可以視需要直接將它與 SQL Server Management Studio 等工具連線。</span><span class="sxs-lookup"><span data-stu-id="5e60b-137">The console output should validate that the server was created and works as expected, but you can connect to it directly with a tool like SQL Server Management Studio if you like.</span></span>

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="5e60b-138">將 blob 寫入新的儲存體帳戶中</span><span class="sxs-lookup"><span data-stu-id="5e60b-138">Write a blob into a new storage account</span></span>

<span data-ttu-id="5e60b-139">這個範例會建立儲存體帳戶，並上傳 blob。</span><span class="sxs-lookup"><span data-stu-id="5e60b-139">This example will create a storage account and upload a blob.</span></span>  

<span data-ttu-id="5e60b-140">使用下列項目來取代 `Main` 方法。</span><span class="sxs-lookup"><span data-stu-id="5e60b-140">Replace the `Main` method with the following.</span></span>

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string storageAccountName = SdkContext.RandomResourceName("st", 10);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the storage account
    Console.WriteLine("Creating storage account...");
    var storage = azure.StorageAccounts.Define(storageAccountName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .Create();

    var storageKeys = storage.GetKeys();
    string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

    var account = CloudStorageAccount.Parse(storageConnectionString);
    var serviceClient = account.CreateCloudBlobClient();
    
    // Create container. Name must be lower case.
    Console.WriteLine("Creating container...");
    var container = serviceClient.GetContainerReference("helloazure");
    container.CreateIfNotExistsAsync().Wait();

    // Make the container public
    var containerPermissions = new BlobContainerPermissions()
        { PublicAccess = BlobContainerPublicAccessType.Container };
    container.SetPermissionsAsync(containerPermissions).Wait();
    
    // write a blob to the container
    Console.WriteLine("Uploading blob...");
    var blob = container.GetBlockBlobReference("helloazure.txt");
    blob.UploadTextAsync("Hello, Azure!").Wait();
    Console.WriteLine("Your blob is located at {0}", blob.StorageUri.PrimaryUri);

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();        
}
```

<span data-ttu-id="5e60b-141">按 **F5** 以執行範例。</span><span class="sxs-lookup"><span data-stu-id="5e60b-141">Press **F5** to run the sample.</span></span>

<span data-ttu-id="5e60b-142">幾分鐘之後，程式就會完成。</span><span class="sxs-lookup"><span data-stu-id="5e60b-142">After several minutes, the program will finish.</span></span> <span data-ttu-id="5e60b-143">瀏覽至主控台中顯示的 URL，即可確認已上傳 blob。</span><span class="sxs-lookup"><span data-stu-id="5e60b-143">Verify the blob was uploaded by browsing to the URL displayed in the console.</span></span>  <span data-ttu-id="5e60b-144">您應該會看到文字 "Hello, Azure!"</span><span class="sxs-lookup"><span data-stu-id="5e60b-144">You should see the text "Hello, Azure!"</span></span> <span data-ttu-id="5e60b-145">在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="5e60b-145">in your browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="5e60b-146">清除</span><span class="sxs-lookup"><span data-stu-id="5e60b-146">Clean up</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e60b-147">如果您未從本教學課程中清除資源，就必須繼續支付它們。</span><span class="sxs-lookup"><span data-stu-id="5e60b-147">If you don't clean up your resources from this tutorial, you will continue to be charged for them.</span></span>  <span data-ttu-id="5e60b-148">請務必進行此步驟。</span><span class="sxs-lookup"><span data-stu-id="5e60b-148">Be sure to do this step.</span></span>

<span data-ttu-id="5e60b-149">刪除您所建立的所有資源，方法是在 PowerShell 中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="5e60b-149">Delete all the resources you created by entering the following in PowerShell:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName sampleResourceGroup
```
## <a name="explore-more-samples"></a><span data-ttu-id="5e60b-150">探索更多範例</span><span class="sxs-lookup"><span data-stu-id="5e60b-150">Explore more samples</span></span>

<span data-ttu-id="5e60b-151">若要深入了解如何使用適用於 .NET 的 Azure 程式庫來管理資源和自動執行工作，請參閱我們針對[虛擬機器](dotnet-sdk-azure-virtual-machine-samples.md)、[Web 應用程式](dotnet-sdk-azure-web-apps-samples.md)和 [SQL Database](dotnet-sdk-azure-sql-database-samples.md) 所提供的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="5e60b-151">To learn more about how to use the Azure libraries for .NET to manage resources and automate tasks, see our sample code for [virtual machines](dotnet-sdk-azure-virtual-machine-samples.md), [web apps](dotnet-sdk-azure-web-apps-samples.md) and [SQL database](dotnet-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference"></a><span data-ttu-id="5e60b-152">參考</span><span class="sxs-lookup"><span data-stu-id="5e60b-152">Reference</span></span>

<span data-ttu-id="5e60b-153">我們針對所有套件提供了[參考資料](http://docs.microsoft.com/dotnet/api)。</span><span class="sxs-lookup"><span data-stu-id="5e60b-153">A [reference](http://docs.microsoft.com/dotnet/api) is available for all packages.</span></span>

[!include[Contribute and community](includes/contribute.md)]
