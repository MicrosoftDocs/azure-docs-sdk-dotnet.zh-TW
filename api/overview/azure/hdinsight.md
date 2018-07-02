---
title: 適用於 .NET 的 Azure HDInsight 程式庫
description: 適用於 .NET 的 Azure HDInsight 程式庫參考
keywords: Azure, .NET, SDK, API, HDInsight
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: hd-insight
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2cdb080b4d224a77a36318cefd13ebfae2e3e2e1
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065808"
---
# <a name="azure-hdinsight-libraries-for-net"></a>適用於 .NET 的 Azure HDInsight 程式庫

## <a name="overview"></a>概觀

HDInsight 服務 .NET SDK 提供與建立、設定、提交和監視 Azure HDInsight 服務所管理之 Hadoop 工作相關的類別。 此外，它會提供類別來管理使用 HDInsight 服務的 Azure 訂用帳戶，並設定叢集、儲存體帳戶和其他 Azure 訂用帳戶所管理之 HDInsight 叢集相關聯的資產。

## <a name="management-libraries"></a>管理程式庫

### <a name="jobs"></a>工作

使用 Azure HDInsight 用戶端 SDK 來建立、管理和監視在 Hadoop 叢集上的作業。 

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a>程式碼範例

這個範例會在 Hadoop 叢集中執行 Hive 作業。

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

### <a name="hdinsight"></a>HDInsight

使用 Azure HDInsight 管理 SDK 來建立、管理、啟動、停止和調整 Hadoop 叢集。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a>程式碼範例

這個範例會使用現有的 Azure Blob 儲存體來建立 HDInsight 兩個節點 Linux Hadoop 叢集。

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
> [探索管理 API](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a>範例

- [叢集建立](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [叢集管理](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [執行 Hive 作業](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [執行 Pig 作業](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [更多作業](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

檢視 Azure SQL Database 範例的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
