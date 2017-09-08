---
title: "開始使用 Azure .NET API"
description: "使用自有 Azure 訂用帳戶開始進行適用於 .NET 之 Azure 程式庫的基本使用。"
keywords: "Azure, .NET, SDK, API , 驗證, 開始使用"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 0379609e863c674de4518d5ed615b6b4f9c46a12
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="get-started-with-the-azure-net-apis"></a>開始使用適用於 .NET 的 Azure SDK

本教學課程會示範數個[適用於 .NET 的 Azure API](/dotnet/api/overview/azure/)使用方式。  您將設定驗證、建立和使用 Azure 儲存體帳戶、建立和使用 Azure SQL Database、部署部分的虛擬機器，以及從 GitHub 部署 Azure App Service Web 應用程式。

## <a name="prerequisites"></a>必要條件

- 一個 Azure 帳戶。 如果您沒有帳戶，請[取得免費試用帳戶](https://azure.microsoft.com/free/)
- [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="set-up-authentication"></a>設定驗證

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a>建立新專案 

這會建立新的主控台應用程式專案。  在 Visual Studio 中，按一下 [檔案]、[新增]，然後按一下 [專案...] 來這麼做。在 Visual C# 範本下，選取 [主控台應用程式 (.NET Core)]、命名您的專案，然後按一下 [確定]。

![[新增專案] 對話方塊](media/dotnet-sdk-azure-get-started/new-project.png)

建立新的主控台應用程式時，可開啟「套件管理員主控台」，方法是按一下 [工具]、[NuGet 套件管理員]，然後按一下 [套件管理員主控台]。  在主控台中，可執行下列三個命令來取得您需要的套件：

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a>指示詞

編輯應用程式的 `Program.cs` 檔案。  使用下列內容取代頂端的 `using` 指示詞：

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

## <a name="create-a-virtual-machine"></a>建立虛擬機器

此範例會部署虛擬機器。 

使用下列項目來取代 `Main` 方法。  務必提供虛擬機器的實際 `username` 和 `password`。

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

按 **F5** 以執行範例。

幾分鐘之後，程式就會完成，提示您按下輸入。 按下輸入後，使用 PowerShell 來確認您訂用帳戶中的虛擬機器：

```powershell
Get-AzureRmVm -ResourceGroupName sampleResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>從 GitHub 存放庫部署 Web 應用程式

現在，您將修改程式碼，從現有的 GitHub 存放庫建立部署新的 web 應用程式。 以下列程式碼取代 `Main` 方法：

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

如過去一樣，按下 **F5** 來執行程式碼。  開啟瀏覽器並瀏覽至主控台中顯示的 URL，即可驗證部署。

## <a name="connect-to-a-sql-database"></a>連線到 SQL Database

此範例會建立新的 Azure SQL Database，並執行一些 SQL 作業。

使用下列項目取代 `Main` 方法，並確認指派 `dbPassword` 的強式密碼：

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
如過去一樣，按下 **F5** 來執行程式碼。  主控台輸出應該要驗證伺服器已建立並如預期運作，但您可以視需要直接將它與 SQL Server Management Studio 等工具連線。

## <a name="write-a-blob-into-a-new-storage-account"></a>將 blob 寫入新的儲存體帳戶中

這個範例會建立儲存體帳戶，並上傳 blob。  

使用下列項目來取代 `Main` 方法。

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

按 **F5** 以執行範例。

幾分鐘之後，程式就會完成。 瀏覽至主控台中顯示的 URL，即可確認已上傳 blob。  您應該會看到文字 "Hello, Azure!" 在瀏覽器中。

## <a name="clean-up"></a>清除

> [!IMPORTANT]
> 如果您未從本教學課程中清除資源，就必須繼續支付它們。  請務必進行此步驟。

刪除您所建立的所有資源，方法是在 PowerShell 中輸入下列命令：

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName sampleResourceGroup
```
## <a name="explore-more-samples"></a>探索更多範例

若要深入了解如何使用適用於 .NET 的 Azure 程式庫來管理資源和自動執行工作，請參閱我們針對[虛擬機器](dotnet-sdk-azure-virtual-machine-samples.md)、[Web 應用程式](dotnet-sdk-azure-web-apps-samples.md)和 [SQL Database](dotnet-sdk-azure-sql-database-samples.md) 所提供的程式碼範例。

## <a name="reference"></a>參考

我們針對所有套件提供了[參考資料](http://docs.microsoft.com/dotnet/api)。

[!include[Contribute and community](includes/contribute.md)]
