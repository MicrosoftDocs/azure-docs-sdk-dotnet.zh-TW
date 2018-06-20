---
title: 適用於 .NET 的 Azure HDInsight 程式庫
description: 適用於 .NET 的 Azure HDInsight 程式庫參考
keywords: Azure, .NET, SDK, API, HDInsight
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: hd-insight
ms.custom: devcenter, svc-overview
ms.openlocfilehash: da9023ab4e6106754d48acb31cda58cdb358f5cb
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2017
ms.locfileid: "23486951"
---
# <a name="azure-hdinsight-libraries-for-net"></a><span data-ttu-id="3aadc-104">適用於 .NET 的 Azure HDInsight 程式庫</span><span class="sxs-lookup"><span data-stu-id="3aadc-104">Azure HDInsight libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3aadc-105">概觀</span><span class="sxs-lookup"><span data-stu-id="3aadc-105">Overview</span></span>

<span data-ttu-id="3aadc-106">HDInsight 服務 .NET SDK 提供與建立、設定、提交和監視 Azure HDInsight 服務所管理之 Hadoop 工作相關的類別。</span><span class="sxs-lookup"><span data-stu-id="3aadc-106">The HDInsight Service .NET SDK provides classes that relate to the creation, configuration, submission, and monitoring of Hadoop jobs managed by an Azure HDInsight Service.</span></span> <span data-ttu-id="3aadc-107">此外，它會提供類別來管理使用 HDInsight 服務的 Azure 訂用帳戶，並設定叢集、儲存體帳戶和其他 Azure 訂用帳戶所管理之 HDInsight 叢集相關聯的資產。</span><span class="sxs-lookup"><span data-stu-id="3aadc-107">In addition, it provides classes to manage Azure subscriptions using the HDInsight Service and to configure the clusters, storage accounts, and other assets associated with the HDInsight clusters that are managed by an Azure subscription.</span></span>

## <a name="management-libraries"></a><span data-ttu-id="3aadc-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="3aadc-108">Management libraries</span></span>

### <a name="jobs"></a><span data-ttu-id="3aadc-109">工作</span><span class="sxs-lookup"><span data-stu-id="3aadc-109">Jobs</span></span>

<span data-ttu-id="3aadc-110">使用 Azure HDInsight 用戶端 SDK 來建立、管理和監視在 Hadoop 叢集上的作業。</span><span class="sxs-lookup"><span data-stu-id="3aadc-110">Use the Azure HDInsight client SDK to create, manage, and monitor jobs on a Hadoop cluster.</span></span> 

<span data-ttu-id="3aadc-111">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="3aadc-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3aadc-112">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="3aadc-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a><span data-ttu-id="3aadc-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="3aadc-113">Code Example</span></span>

<span data-ttu-id="3aadc-114">這個範例會在 Hadoop 叢集中執行 Hive 作業。</span><span class="sxs-lookup"><span data-stu-id="3aadc-114">This example runs a Hive job in a Hadoop cluster.</span></span>

```csharp
HDInsightJobManagementClient managementClient = new HDInsightJobManagementClient(clusterUri, credentials);

Dictionary<string, string> defines = new Dictionary<string, string> {
    { "hive.execution.engine", "tez" },
    { "hive.exec.reducers.max", "1" }
};
List<string> arguments = new List<string> { { "argA" }, { "argB" } };
HiveJobSubmissionParameters parameters = new HiveJobSubmissionParameters
{
    Query = "SHOW TABLES",
    Defines = defines,
    Arguments = arguments
};

JobSubmissionResponse jobResponse = managementClient.JobManagement.SubmitHiveJob(parameters);
```

### <a name="hdinsight"></a><span data-ttu-id="3aadc-115">HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aadc-115">HDInsight</span></span>

<span data-ttu-id="3aadc-116">使用 Azure HDInsight 管理 SDK 來建立、管理、啟動、停止和調整 Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="3aadc-116">Use the Azure HDInsight management SDK to create, manage, start, stop, and scale Hadoop clusters.</span></span>

<span data-ttu-id="3aadc-117">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="3aadc-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3aadc-118">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="3aadc-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a><span data-ttu-id="3aadc-119">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="3aadc-119">Code Example</span></span>

<span data-ttu-id="3aadc-120">這個範例會使用現有的 Azure Blob 儲存體來建立 HDInsight 兩個節點 Linux Hadoop 叢集。</span><span class="sxs-lookup"><span data-stu-id="3aadc-120">This example creates an HDInsight two node Linux Hadoop cluster with an existing Azure Blob Storage.</span></span>

```csharp
HDInsightManagementClient managementClient = new HDInsightManagementClient(authToken);
// Set parameters for the new cluster
ClusterCreateParameters parameters = new ClusterCreateParameters
{
    ClusterSizeInNodes = 2,
    UserName = "admin",
    Password = "<Enter HTTP User Password>",
    ClusterType = "Hadoop",
    OSType = OSType.Linux,
    Version = "3.5",
    // Use an Azure storage account as the default storage
    DefaultStorageInfo = new AzureStorageInfo("<StorageAccount>", "<StorageKey>", "<BlobContainerName>"),
    Location = "EAST US 2",
    SshUserName = "sshuser",
    SshPassword = "<Enter SSH User Password>",
};

// Create the cluster
managementClient.Clusters.Create("<ExistingResourceGroupName>", "<NewClusterName>", parameters);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3aadc-121">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="3aadc-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a><span data-ttu-id="3aadc-122">範例</span><span class="sxs-lookup"><span data-stu-id="3aadc-122">Samples</span></span>

- [<span data-ttu-id="3aadc-123">叢集建立</span><span class="sxs-lookup"><span data-stu-id="3aadc-123">Cluster creation</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [<span data-ttu-id="3aadc-124">叢集管理</span><span class="sxs-lookup"><span data-stu-id="3aadc-124">Cluster management</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [<span data-ttu-id="3aadc-125">執行 Hive 作業</span><span class="sxs-lookup"><span data-stu-id="3aadc-125">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="3aadc-126">執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="3aadc-126">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="3aadc-127">更多作業</span><span class="sxs-lookup"><span data-stu-id="3aadc-127">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

<span data-ttu-id="3aadc-128">檢視 Azure SQL Database 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight)。</span><span class="sxs-lookup"><span data-stu-id="3aadc-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) of Azure SQL Database samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
