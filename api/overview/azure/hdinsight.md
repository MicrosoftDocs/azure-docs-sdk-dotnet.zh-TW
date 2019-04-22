---
title: 適用於.NET 的 Azure HDInsight SDK
description: 適用於 .NET 的 Azure HDInsight SDK 參考
ms.date: 04/10/2019
ms.topic: reference
ms.service: hdinsight
ms.openlocfilehash: 2282a302b269a52c71ed88c26e021344cdca4382
ms.sourcegitcommit: 4328168172ac1b1a448e16988f75199262bc5c2d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/17/2019
ms.locfileid: "59700256"
---
# <a name="azure-hdinsight-sdk-for-net"></a><span data-ttu-id="25f7f-103">適用於.NET 的 Azure HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="25f7f-103">Azure HDInsight SDK for .NET</span></span>

<span data-ttu-id="25f7f-104">Azure HDInsight 會提供適用於 .NET 的管理和作業 SDK，並提供類別以管理您的 HDInsight 叢集並提交和監視 Hadoop 作業。</span><span class="sxs-lookup"><span data-stu-id="25f7f-104">Azure HDInsight offers management and job SDKs for .NET that provide classes for managing your HDInsight cluster and submitting and monitoring Hadoop jobs.</span></span>

## <a name="management"></a><span data-ttu-id="25f7f-105">管理性</span><span class="sxs-lookup"><span data-stu-id="25f7f-105">Management</span></span>

<span data-ttu-id="25f7f-106">適用於 .NET 的 HDInsight 管理 SDK 提供可讓您管理 HDInsight 叢集的類別和方法。</span><span class="sxs-lookup"><span data-stu-id="25f7f-106">The HDInsight management SDK for .NET provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="25f7f-107">它包含用來建立、刪除、更新、列出、調整大小、執行指令碼動作、監視、取得 HDInsight 叢集屬性的作業，和其他多種作業。</span><span class="sxs-lookup"><span data-stu-id="25f7f-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25f7f-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="25f7f-108">Prerequisites</span></span>

* <span data-ttu-id="25f7f-109">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="25f7f-109">An Azure account.</span></span> <span data-ttu-id="25f7f-110">如果您沒有帳戶，請[取得免費試用帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="25f7f-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="25f7f-111">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="25f7f-111">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a><span data-ttu-id="25f7f-112">SDK 安裝</span><span class="sxs-lookup"><span data-stu-id="25f7f-112">SDK Installation</span></span>

<span data-ttu-id="25f7f-113">在 Visual Studio 專案中開啟套件管理員主控台，方法是按一下 [工具]、[NuGet 套件管理員]，然後按一下 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="25f7f-113">From your Visual Studio project, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>

<span data-ttu-id="25f7f-114">在套件管理員主控台中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="25f7f-114">In the Package Manager Console, execute the following commands:</span></span>

```
  Install-Package Microsoft.Azure.Management.HDInsight
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a><span data-ttu-id="25f7f-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="25f7f-115">Authentication</span></span>

<span data-ttu-id="25f7f-116">SDK 必須先使用您的 Azure 訂用帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="25f7f-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="25f7f-117">請依照下列範例建立服務主體，並使用它來驗證。</span><span class="sxs-lookup"><span data-stu-id="25f7f-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="25f7f-118">此動作完成後，您會有 `HDInsightManagementClient` 的執行個體，其中包含許多可用來執行管理作業的方法 (分述於下列各節中)。</span><span class="sxs-lookup"><span data-stu-id="25f7f-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="25f7f-119">除了下列範例以外，還有其他方式可進行驗證，可能更符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="25f7f-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="25f7f-120">此處概述所有方法：[使用適用於 .NET 的 Azure 程式庫進行驗證](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="25f7f-120">All methods are outlined here: [Authenticate with the Azure Libraries for .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="25f7f-121">使用服務主體的驗證範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="25f7f-122">首先，請登入 [Azure Cloud Shell](https://shell.azure.com/bash)。</span><span class="sxs-lookup"><span data-stu-id="25f7f-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="25f7f-123">確認您目前使用的訂用帳戶，是您希望建立服務主體的位置。</span><span class="sxs-lookup"><span data-stu-id="25f7f-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="25f7f-124">您的訂用帳戶資訊會以 JSON 的形式顯示。</span><span class="sxs-lookup"><span data-stu-id="25f7f-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="25f7f-125">如果您未登入正確的訂用帳戶，請執行下列命令以選取正確的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="25f7f-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="25f7f-126">如果您尚未以其他方法註冊 HDInsight 資源提供者 (例如，透過 Azure 入口網站建立 HDInsight 叢集)，您必須立即執行此動作，才能進行驗證。</span><span class="sxs-lookup"><span data-stu-id="25f7f-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="25f7f-127">此動作也可以從 [Azure Cloud Shell](https://shell.azure.com/bash) 完成，只要執行下列命令即可：</span><span class="sxs-lookup"><span data-stu-id="25f7f-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="25f7f-128">接下來，請選擇服務主體的名稱，並使用下列命令加以建立：</span><span class="sxs-lookup"><span data-stu-id="25f7f-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="25f7f-129">服務主體資訊會顯示為 JSON。</span><span class="sxs-lookup"><span data-stu-id="25f7f-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="25f7f-130">複製下列程式碼片段，並且在 `TENANT_ID`、`CLIENT_ID`、`CLIENT_SECRET` 和 `SUBSCRIPTION_ID` 中填入在執行建立服務主體的命令後傳回的 JSON 中所包含的字串。</span><span class="sxs-lookup"><span data-stu-id="25f7f-130">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

## <a name="cluster-management"></a><span data-ttu-id="25f7f-131">叢集管理</span><span class="sxs-lookup"><span data-stu-id="25f7f-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="25f7f-132">本節假設您已通過驗證並建構 `HDInsightManagementClient` 執行個體，並且將其儲存在名為 `client` 的變數中。</span><span class="sxs-lookup"><span data-stu-id="25f7f-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="25f7f-133">驗證及取得 `HDInsightManagementClient` 的指示可在先前的「驗證」一節中找到。</span><span class="sxs-lookup"><span data-stu-id="25f7f-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="25f7f-134">建立叢集</span><span class="sxs-lookup"><span data-stu-id="25f7f-134">Create a Cluster</span></span>

<span data-ttu-id="25f7f-135">新叢集可藉由呼叫 `client.Clusters.Create()` 來建立。</span><span class="sxs-lookup"><span data-stu-id="25f7f-135">A new cluster can be created by calling `client.Clusters.Create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="25f7f-136">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-136">Samples</span></span>

<span data-ttu-id="25f7f-137">這裡提供建立數個常見 HDInsight 叢集類型的程式碼範例：[HDInsight .NET 範例](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="25f7f-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight .NET Samples](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="25f7f-138">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-138">Example</span></span>

<span data-ttu-id="25f7f-139">此範例示範如何使用 2 個前端節點和 1 個背景工作節點來建立 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="25f7f-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="25f7f-140">您必須先建立資源群組和儲存體帳戶，說明如下。</span><span class="sxs-lookup"><span data-stu-id="25f7f-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="25f7f-141">如果您已建立這些項目，則可以略過這些步驟。</span><span class="sxs-lookup"><span data-stu-id="25f7f-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="25f7f-142">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="25f7f-142">Creating a Resource Group</span></span>

<span data-ttu-id="25f7f-143">您可以使用 [Azure Cloud Shell](https://shell.azure.com/bash) 建立資源群組，只要執行下列命令即可</span><span class="sxs-lookup"><span data-stu-id="25f7f-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="25f7f-144">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="25f7f-144">Creating a Storage Account</span></span>

<span data-ttu-id="25f7f-145">您可以使用 [Azure Cloud Shell](https://shell.azure.com/bash) 建立儲存體帳戶，只要執行下列命令即可：</span><span class="sxs-lookup"><span data-stu-id="25f7f-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="25f7f-146">現在請執行下列命令，以取得儲存體帳戶的金鑰 (您需要此金鑰才能建立叢集)：</span><span class="sxs-lookup"><span data-stu-id="25f7f-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="25f7f-147">下列 .NET 程式碼片段會使用 2 個前端節點和 1 個背景工作節點來建立 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="25f7f-147">The below .NET snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="25f7f-148">請依照註解中的說明填入空白變數，並依據您的特定需求變更其他參數。</span><span class="sxs-lookup"><span data-stu-id="25f7f-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="25f7f-149">取得叢集詳細資料</span><span class="sxs-lookup"><span data-stu-id="25f7f-149">Get Cluster Details</span></span>

<span data-ttu-id="25f7f-150">若要取得特定叢集的屬性：</span><span class="sxs-lookup"><span data-stu-id="25f7f-150">To get properties for a given cluster:</span></span>

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="25f7f-151">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-151">Example</span></span>

<span data-ttu-id="25f7f-152">您可以使用 `get` 來確認您已成功建立叢集。</span><span class="sxs-lookup"><span data-stu-id="25f7f-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

<span data-ttu-id="25f7f-153">輸出應會顯示如下：</span><span class="sxs-lookup"><span data-stu-id="25f7f-153">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> <span data-ttu-id="25f7f-154">`get` 的傳回值會儲存在變數 `myCluster` 中，且屬於 `Microsoft.Azure.Management.HDInsight.ModelsCluster` 類型。</span><span class="sxs-lookup"><span data-stu-id="25f7f-154">The return value of `get`, stored in variable `myCluster`, is of type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span></span> <span data-ttu-id="25f7f-155">您可以在[此處](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview)找到此物件的完整屬性清單。</span><span class="sxs-lookup"><span data-stu-id="25f7f-155">A full list of this object's properties can be found [here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span></span>


### <a name="list-clusters"></a><span data-ttu-id="25f7f-156">列出叢集</span><span class="sxs-lookup"><span data-stu-id="25f7f-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="25f7f-157">列出訂用帳戶下的叢集</span><span class="sxs-lookup"><span data-stu-id="25f7f-157">List Clusters Under The Subscription</span></span>

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="25f7f-158">依資源群組列出叢集</span><span class="sxs-lookup"><span data-stu-id="25f7f-158">List Clusters By Resource Group</span></span>

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="25f7f-159">`List()` 和 `ListByResourceGroup()` 都會傳回 `IPage<Cluster>` 物件。</span><span class="sxs-lookup"><span data-stu-id="25f7f-159">Both `List()` and `ListByResourceGroup()` return an `IPage<Cluster>` object.</span></span> <span data-ttu-id="25f7f-160">若要取得下一個頁面，您可以呼叫 `client.Clusters.ListNext("Next Page Link")`。</span><span class="sxs-lookup"><span data-stu-id="25f7f-160">To get the next page, you can call `client.Clusters.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="25f7f-161">此動作可重複直到 `NextPageLink` 成為 `null`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="25f7f-161">This can be repeated until `NextPageLink` is `null`, as shown in the example below.</span></span>

#### <a name="example"></a><span data-ttu-id="25f7f-162">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-162">Example</span></span>
<span data-ttu-id="25f7f-163">下列範例會列印目前訂用帳戶所有叢集的屬性：</span><span class="sxs-lookup"><span data-stu-id="25f7f-163">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="25f7f-164">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="25f7f-164">Delete a Cluster</span></span>

<span data-ttu-id="25f7f-165">若要刪除叢集：</span><span class="sxs-lookup"><span data-stu-id="25f7f-165">To delete a cluster:</span></span>

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="25f7f-166">更新叢集標記</span><span class="sxs-lookup"><span data-stu-id="25f7f-166">Update Cluster Tags</span></span>

<span data-ttu-id="25f7f-167">您可以更新指定叢集的標記，如下所示：</span><span class="sxs-lookup"><span data-stu-id="25f7f-167">You can update the tags of a given cluster like so:</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a><span data-ttu-id="25f7f-168">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-168">Example</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a><span data-ttu-id="25f7f-169">調整叢集大小</span><span class="sxs-lookup"><span data-stu-id="25f7f-169">Resize Cluster</span></span>

<span data-ttu-id="25f7f-170">您可以藉由指定新的大小來調整指定叢集的背景工作節點數目，如下所示：</span><span class="sxs-lookup"><span data-stu-id="25f7f-170">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="25f7f-171">叢集監視</span><span class="sxs-lookup"><span data-stu-id="25f7f-171">Cluster Monitoring</span></span>

<span data-ttu-id="25f7f-172">HDInsight 管理 SDK 也可用來透過 Operations Management Suite (OMS) 管理您對叢集的監視。</span><span class="sxs-lookup"><span data-stu-id="25f7f-172">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="25f7f-173">啟用 OMS 監視</span><span class="sxs-lookup"><span data-stu-id="25f7f-173">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="25f7f-174">若要啟用 OMS 監視，您必須擁有現有的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="25f7f-174">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="25f7f-175">如果您尚未建立工作區，您可以在此了解如何建立：[在 Azure 入口網站中建立 Log Analytics 工作區](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace)。</span><span class="sxs-lookup"><span data-stu-id="25f7f-175">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="25f7f-176">若要對您的叢集啟用 OMS 監視：</span><span class="sxs-lookup"><span data-stu-id="25f7f-176">To enable OMS Monitoring on your cluster:</span></span>

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="25f7f-177">檢視 OMS 監視的狀態</span><span class="sxs-lookup"><span data-stu-id="25f7f-177">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="25f7f-178">若要取得叢集的 OMS 狀態：</span><span class="sxs-lookup"><span data-stu-id="25f7f-178">To get the status of OMS on your cluster:</span></span>

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="25f7f-179">停用 OMS 監視</span><span class="sxs-lookup"><span data-stu-id="25f7f-179">Disable OMS Monitoring</span></span>

<span data-ttu-id="25f7f-180">若要對您的叢集停用 OMS：</span><span class="sxs-lookup"><span data-stu-id="25f7f-180">To disable OMS on your cluster:</span></span>

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="25f7f-181">指令碼動作</span><span class="sxs-lookup"><span data-stu-id="25f7f-181">Script Actions</span></span>

<span data-ttu-id="25f7f-182">HDInsight 提供名為指令碼動作的設定方法，此方法會叫用自訂指令碼來自訂叢集。</span><span class="sxs-lookup"><span data-stu-id="25f7f-182">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="25f7f-183">您可以在此處找到如何使用指令碼動作的詳細資訊：[使用指令碼動作自訂 Linux 型 HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="25f7f-183">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="25f7f-184">執行指令碼動作</span><span class="sxs-lookup"><span data-stu-id="25f7f-184">Execute Script Actions</span></span>

<span data-ttu-id="25f7f-185">您可以對指定的叢集執行指令碼動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="25f7f-185">You can execute script actions on a given cluster like so:</span></span>

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="25f7f-186">刪除指令碼動作</span><span class="sxs-lookup"><span data-stu-id="25f7f-186">Delete Script Action</span></span>

<span data-ttu-id="25f7f-187">若要刪除對給定叢集指定的持續性指令碼動作：</span><span class="sxs-lookup"><span data-stu-id="25f7f-187">To delete a specified persisted script action on a given cluster:</span></span>

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="25f7f-188">列出持續性指令碼動作</span><span class="sxs-lookup"><span data-stu-id="25f7f-188">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="25f7f-189">`ListPersistedScripts()` 和 `List()` 會傳回 `IPage<RuntimeScriptActionDetail>` 物件。</span><span class="sxs-lookup"><span data-stu-id="25f7f-189">`ListPersistedScripts()` and `List()` return an `IPage<RuntimeScriptActionDetail>` object.</span></span> <span data-ttu-id="25f7f-190">若要取得下一個頁面，您可以呼叫 `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` 或 `client.ScriptExecutionHistory.ListNext("Next Page Link")`。</span><span class="sxs-lookup"><span data-stu-id="25f7f-190">To get the next page, you can call `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` or `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="25f7f-191">此動作可重複直到 `NextPageLink` 成為 `null`，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="25f7f-191">This can be repeated until `NextPageLink` is `null`, as shown in the examples below.</span></span>

<span data-ttu-id="25f7f-192">若要列出指定叢集的所有持續性指令碼動作：</span><span class="sxs-lookup"><span data-stu-id="25f7f-192">To list all persisted script actions for the specified cluster:</span></span>
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="25f7f-193">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-193">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="25f7f-194">列出所有指令碼的執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="25f7f-194">List All Scripts' Execution History</span></span>

<span data-ttu-id="25f7f-195">若要針對指定的叢集列出所有指令碼的執行歷程記錄：</span><span class="sxs-lookup"><span data-stu-id="25f7f-195">To list all scripts' execution history for the specified cluster:</span></span>

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="25f7f-196">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-196">Example</span></span>

<span data-ttu-id="25f7f-197">此範例會列印過去所有指令碼執行的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="25f7f-197">This example prints all the details for all past script executions.</span></span>

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

## <a name="jobs"></a><span data-ttu-id="25f7f-198">工作</span><span class="sxs-lookup"><span data-stu-id="25f7f-198">Jobs</span></span>

<span data-ttu-id="25f7f-199">使用適用於 .NET 的 Azure HDInsight 作業 SDK 來建立、管理和監視在 Hadoop 叢集上的作業。</span><span class="sxs-lookup"><span data-stu-id="25f7f-199">Use the Azure HDInsight job SDK for .NET to create, manage, and monitor jobs on a Hadoop cluster.</span></span>

### <a name="sdk-installation"></a><span data-ttu-id="25f7f-200">SDK 安裝</span><span class="sxs-lookup"><span data-stu-id="25f7f-200">SDK Installation</span></span>

<span data-ttu-id="25f7f-201">直接從 Visual Studio [套件管理員主控台][PackageManager] 安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="25f7f-201">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="25f7f-202">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="25f7f-202">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

### <a name="code-example"></a><span data-ttu-id="25f7f-203">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-203">Code Example</span></span>

<span data-ttu-id="25f7f-204">這個範例會在 Hadoop 叢集中執行 Hive 作業。</span><span class="sxs-lookup"><span data-stu-id="25f7f-204">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="samples"></a><span data-ttu-id="25f7f-205">範例</span><span class="sxs-lookup"><span data-stu-id="25f7f-205">Samples</span></span>

- [<span data-ttu-id="25f7f-206">執行 Hive 作業</span><span class="sxs-lookup"><span data-stu-id="25f7f-206">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="25f7f-207">執行 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="25f7f-207">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="25f7f-208">更多作業</span><span class="sxs-lookup"><span data-stu-id="25f7f-208">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)
