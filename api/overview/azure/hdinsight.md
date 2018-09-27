---
title: Azure HDInsight .NET SDK
description: Azure HDInsight .NET SDK 的參考
ms.date: 9/19/2018
ms.topic: reference
ms.service: hd-insight
ms.openlocfilehash: d25bdb1c9086cd93190b97f519654f2c193b9dc3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190681"
---
# <a name="azure-hdinsight-net-sdk"></a>Azure HDInsight .NET SDK

## <a name="azure-hdinsight-libraries-for-net-2x"></a>適用於 .NET 2.X 的 Azure HDInsight 程式庫

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

## <a name="hdinsight-net-management-sdk-3x-preview"></a>HDInsight .NET 管理 SDK 3.X 預覽版

## <a name="overview"></a>概觀

HDInsight .NET SDK 提供可讓您管理 HDInsight 叢集的類別和方法。 它包含用來建立、刪除、更新、列出、調整、執行指令碼動作、監視、取得 HDInsight 叢集屬性的作業，和其他多種作業。

## <a name="prerequisites"></a>必要條件

* 一個 Azure 帳戶。 如果您沒有帳戶，請[取得免費試用帳戶](https://azure.microsoft.com/free/)。
* [Visual Studio](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a>SDK 安裝

在 Visual Studio 專案中開啟套件管理員主控台，方法是按一下 [工具]、[NuGet 套件管理員]，然後按一下 [套件管理員主控台]。

在套件管理員主控台中，執行下列命令：

```
  Install-Package Microsoft.Azure.Management.HDInsight -Version 3.1.0-preview
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a>驗證

SDK 必須先使用您的 Azure 訂用帳戶進行驗證。  請依照下列範例建立服務主體，並使用它來驗證。 此動作完成後，您會有 `HDInsightManagementClient` 的執行個體，其中包含許多可用來執行管理作業的方法 (分述於下列各節中)。

> [!NOTE]
> 除了下列範例以外，還有其他方式可進行驗證，可能更符合您的需求。 所有方法皆概述於此處：[使用適用於 .NET 的 Azure 程式庫來進行驗證](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)

### <a name="authentication-example-using-a-service-principal"></a>使用服務主體的驗證範例

首先，請登入 [Azure Cloud Shell](https://shell.azure.com/bash)。 確認您目前使用的訂用帳戶，是您希望建立服務主體的位置。 

```azurecli-interactive
az account show
```

您的訂用帳戶資訊會以 JSON 的形式顯示。

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

如果您未登入正確的訂用帳戶，請執行下列命令以選取正確的訂用帳戶： 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> 如果您尚未以其他方法註冊 HDInsight 資源提供者 (例如，透過 Azure 入口網站建立 HDInsight 叢集)，您必須立即執行此動作，才能進行驗證。 此動作也可以從 [Azure Cloud Shell](https://shell.azure.com/bash) 完成，只要執行下列命令即可：
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

接下來，請選擇服務主體的名稱，並使用下列命令加以建立：

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

服務主體資訊會顯示為 JSON。

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
複製下列程式碼片段，並且在 `TENANT_ID`、`CLIENT_ID`、`CLIENT_SECRET` 和 `SUBSCRIPTION_ID` 中填入在執行建立服務主體的命令後傳回的 JSON 中所包含的字串。

```csharp
using Microsoft.Azure.Management.HDInsight;
using Microsoft.Azure.Management.HDInsight.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent;

namespace HDI_SDK_Test
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tenant ID for your Azure Subscription
            var TENANT_ID = "";
            // Your Service Principal App Client ID
            var CLIENT_ID = "";
            // Your Service Principal Client Secret
            var CLIENT_SECRET = "";
            // Azure Subscription ID
            var SUBSCRIPTION_ID = "";

            var credentials = SdkContext.AzureCredentialsFactory
                .FromServicePrincipal(
                CLIENT_ID,
                CLIENT_SECRET,
                TENANT_ID,
                AzureEnvironment.AzureGlobalCloud);

            var client = new HDInsightManagementClient(credentials);
            client.SubscriptionId = SUBSCRIPTION_ID;
        }
    }
}
```


## <a name="cluster-management"></a>叢集管理

> [!NOTE]
> 本節假設您已通過驗證並建構 `HDInsightManagementClient` 執行個體，並且將其儲存在名為 `client` 的變數中。 驗證及取得 `HDInsightManagementClient` 的指示可在先前的「驗證」一節中找到。

### <a name="create-a-cluster"></a>建立叢集

新叢集可藉由呼叫 `client.Clusters.Create()` 來建立。 

#### <a name="example"></a>範例

此範例示範如何使用 2 個前端節點和 1 個背景工作節點來建立 Spark 叢集。

> [!NOTE]
> 您必須先建立資源群組和儲存體帳戶，說明如下。 如果您已建立這些項目，則可以略過這些步驟。

##### <a name="creating-a-resource-group"></a>建立資源群組

您可以使用 [Azure Cloud Shell](https://shell.azure.com/bash) 建立資源群組，只要執行下列命令即可
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>建立儲存體帳戶

您可以使用 [Azure Cloud Shell](https://shell.azure.com/bash) 建立儲存體帳戶，只要執行下列命令即可：
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
現在請執行下列命令，以取得儲存體帳戶的金鑰 (您需要此金鑰才能建立叢集)：
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
下列 .NET 程式碼片段會使用 2 個前端節點和 1 個背景工作節點來建立 Spark 叢集。 請依照註解中的說明填入空白變數，並依據您的特定需求變更其他參數。

```csharp
// The name for the cluster you are creating
var clusterName = "";
// The name of your existing Resource Group
var resourceGroupName = "";
// Choose a username
var username = "";
// Choose a password
var password = "";
// Replace <> with the name of your storage account
var storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
var storageAccountKey = "";
// Choose a region
var location = "";
var container = "default";

var parameters = new ClusterCreateParametersExtended
{
    Location = location,
    Tags = new Dictionary<string, string>(),
    Properties = new ClusterCreateProperties
    {
        ClusterVersion = "3.6",
        OsType = OSType.Linux,
        ClusterDefinition = new ClusterDefinition
        {
            Kind = "Hadoop",            
            Configurations = new Dictionary<string, Dictionary<string, string>>()
            {                
                { "gateway", new Dictionary<string, string>
                    {
                        { "restAuthCredential.isEnabled", "true" },
                        { "restAuthCredential.username", username},
                        { "restAuthCredential.password", password}
                    }
                }
            }
        },
        Tier = Tier.Standard,
        ComputeProfile = new ComputeProfile
        {
            Roles = new List<Role>{
                new Role
                {
                    Name = "headnode",
                    TargetInstanceCount = 2,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
                new Role
                {
                    Name = "workernode",
                    TargetInstanceCount = 1,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
            }
        },
        StorageProfile = new StorageProfile
        {
            Storageaccounts = new[]
            {
                new StorageAccount
                {
                    Name = storageAccount,
                    Key = storageAccountKey,
                    Container = container,
                    IsDefault = true
                }
            }
        }
    }
};
client.Clusters.Create(
    resourceGroupName,
    clusterName,
    parameters
);
```

### <a name="get-cluster-details"></a>取得叢集詳細資料

若要取得特定叢集的屬性：

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>範例

您可以使用 `get` 來確認您已成功建立叢集。

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

輸出應會顯示如下：

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> `get` 的傳回值會儲存在變數 `myCluster` 中，且屬於 `Microsoft.Azure.Management.HDInsight.ModelsCluster` 類型。 您可以在[此處](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview)找到此物件的完整屬性清單。


### <a name="list-clusters"></a>列出叢集

#### <a name="list-clusters-under-the-subscription"></a>列出訂用帳戶下的叢集

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a>依資源群組列出叢集

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> `List()` 和 `ListByResourceGroup()` 都會傳回 `IPage<Cluster>` 物件。 若要取得下一個頁面，您可以呼叫 `client.Clusters.ListNext("Next Page Link")`。 此動作可重複直到 `NextPageLink` 成為 `null`，如下列範例所示。

#### <a name="example"></a>範例
下列範例會列印目前訂用帳戶所有叢集的屬性：

```csharp
var clustersPaged = client.Clusters.List();
while (true)
{
  foreach (var cluster in clustersPaged)
  {
    Debug.WriteLine(cluster.Name);
  
}  if (clustersPaged.NextPageLink == null)
  {
    break;
  }
  clustersPaged = client.Clusters.ListNext(clustersPaged.NextPageLink);
}
```

### <a name="delete-a-cluster"></a>刪除叢集

若要刪除叢集：

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>更新叢集標記

您可以更新指定叢集的標記，如下所示：

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a>範例

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="scale-cluster"></a>調整叢集

您可以藉由指定新的大小來調整指定叢集的背景工作節點數目，如下所示：

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>叢集監視

HDInsight 管理 SDK 也可用來透過 Operations Management Suite (OMS) 管理您對叢集的監視。

### <a name="enable-oms-monitoring"></a>啟用 OMS 監視

> [!NOTE]
> 若要啟用 OMS 監視，您必須擁有現有的 Log Analytics 工作區。 如果您尚未建立此工作區，您可以參考下列資料了解其建立方式：[在 Azure 入口網站中建立 Log Analytics 工作區](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)。

若要對您的叢集啟用 OMS 監視：

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>檢視 OMS 監視的狀態

若要取得叢集的 OMS 狀態：

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>停用 OMS 監視

若要對您的叢集停用 OMS：

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>指令碼動作

HDInsight 提供名為指令碼動作的設定方法，此方法會叫用自訂指令碼來自訂叢集。
> [!NOTE]
> 如需如何使用指令碼動作的詳細資訊，請參閱：[使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>執行指令碼動作

您可以對指定的叢集執行指令碼動作，如下所示：

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>刪除指令碼動作

若要刪除對給定叢集指定的持續性指令碼動作：

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>列出持續性指令碼動作

> [!NOTE]
> `ListPersistedScripts()` 和 `List()` 會傳回 `IPage<RuntimeScriptActionDetail>` 物件。 若要取得下一個頁面，您可以呼叫 `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` 或 `client.ScriptExecutionHistory.ListNext("Next Page Link")`。 此動作可重複直到 `NextPageLink` 成為 `null`，如下列範例所示。

若要列出指定叢集的所有持續性指令碼動作：
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>範例

```csharp
var scriptsPaged = client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.
    }
    if (scriptsPaged.NextPageLink == null)
    {
        break;
    }
    scriptsPaged = client.ScriptActions.ListPersistedScriptsNext(scriptsPaged.NextPageLink);
}
```

### <a name="list-all-scripts-execution-history"></a>列出所有指令碼的執行歷程記錄

若要針對指定的叢集列出所有指令碼的執行歷程記錄：

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>範例

此範例會列印過去所有指令碼執行的所有詳細資料。

```csharp
var scriptExecutionsPaged = client.ScriptExecutionHistory.List("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptExecutionsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.

    }
    if (scriptExecutionsPaged.NextPageLink == null)
    {
        break;
    }
    scriptExecutionsPaged = client.ScriptExecutionHistory.ListNext(scriptExecutionsPaged.NextPageLink);
}
```
