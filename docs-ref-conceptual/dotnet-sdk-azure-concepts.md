---
title: 適用於 .NET 之 Azure 管理程式庫的使用概念和模式
description: ''
ms.date: 10/19/2017
ms.openlocfilehash: 0a6ae94046680b81f1222c3c2acc6df9871bff4a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190601"
---
# <a name="azure-management-library-for-net-fluent-concepts"></a><span data-ttu-id="0b5b8-102">適用於 .NET Fluent 概念的 Azure 管理程式庫</span><span class="sxs-lookup"><span data-stu-id="0b5b8-102">Azure management library for .NET fluent concepts</span></span>

<span data-ttu-id="0b5b8-103">本文將協助您了解如何有效地在適用於 .NET 的 Azure 管理程式庫中使用 Fluent 介面。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-103">This article will help you understand how to effectively use the fluent interface in the Azure management libraries for .NET.</span></span>

## <a name="building-resources-using-a-fluent-interface"></a><span data-ttu-id="0b5b8-104">使用 Fluent 介面建置資源</span><span class="sxs-lookup"><span data-stu-id="0b5b8-104">Building resources using a fluent interface</span></span>

<span data-ttu-id="0b5b8-105">Fluent 介面是建置者模式的特定表單，會透過強制執行正確資源設定的方法鏈結來建立物件。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-105">A fluent interface is a specific form of the builder pattern that creates objects through a method chain that enforces correct configuration of a resource.</span></span> <span data-ttu-id="0b5b8-106">例如，會使用 Fluent 介面來建立進入點 Azure 物件：</span><span class="sxs-lookup"><span data-stu-id="0b5b8-106">For example, the entry-point Azure object is created using a fluent interface:</span></span>

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a><span data-ttu-id="0b5b8-107">資源集合</span><span class="sxs-lookup"><span data-stu-id="0b5b8-107">Resource collections</span></span>

<span data-ttu-id="0b5b8-108">上面顯示的 `Microsoft.Azure.Management.Fluent.Azure` 物件是 Fluent 管理程式庫中所有資源建立的進入點。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-108">The `Microsoft.Azure.Management.Fluent.Azure` object shown above is the entry point for all resource creation in the fluent management libraries.</span></span> <span data-ttu-id="0b5b8-109">請使用 `Azure` 物件中的資源集合來選取要處理哪種類型的資源。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-109">Select which type of resources to work with using the resource collections in the `Azure` object.</span></span> <span data-ttu-id="0b5b8-110">例如，SQL Database：</span><span class="sxs-lookup"><span data-stu-id="0b5b8-110">For example, for SQL Database:</span></span>

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

<span data-ttu-id="0b5b8-111">如上所示，您與 API 的大部分 Fluent「對話」開頭都會選取您所需 Azure 資源的適當資源集合。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-111">As seen above, most fluent "conversations" you have with the API start with selecting the appropriate resource collection for the Azure resources you need to work with.</span></span>  <span data-ttu-id="0b5b8-112">接著，Visual Studio 中的 Intellisense 會引導您完成交談。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-112">Intellisense in Visual Studio then guides you through the conversation.</span></span> 

![Intellisense 的 GIF 會在 Visual Studio 中進行 Fluent 對話](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a><span data-ttu-id="0b5b8-114">清單和反覆項目</span><span class="sxs-lookup"><span data-stu-id="0b5b8-114">Lists and iterations</span></span>

<span data-ttu-id="0b5b8-115">每個資源集合都會有 `List()` 方法，以便傳回該資源在您目前訂用帳戶中的每個執行個體。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-115">Every resource collection has a `List()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="0b5b8-116">例如，`Azure.SqlServers.List()` 會傳回訂用帳戶中的所有 SQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-116">For example, `Azure.SqlServers.List()` returns all SQL servers in the subscription.</span></span>

<span data-ttu-id="0b5b8-117">使用 `ListByResourceGroup()` 方法可將傳回的清單侷限在特定的 [Azure 資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-117">Use the `ListByResourceGroup()` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="0b5b8-118">請依照您對一般 `List<T>` 所進行的操作方式，來對傳回集合進行反覆執行：</span><span class="sxs-lookup"><span data-stu-id="0b5b8-118">Iterate over the returned collection just as you would a normal `List<T>`:</span></span>

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a><span data-ttu-id="0b5b8-119">可採取動作的動詞</span><span class="sxs-lookup"><span data-stu-id="0b5b8-119">Actionable verbs</span></span>

<span data-ttu-id="0b5b8-120">其名稱中有動詞命令的資源集合方法會在 Azure 中立即採取動作。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-120">Resource collection methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="0b5b8-121">這些方法會同步運作，而且在完成之前會封鎖目前執行緒的執行。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-121">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="0b5b8-122">指令動詞</span><span class="sxs-lookup"><span data-stu-id="0b5b8-122">Verb</span></span>   |  <span data-ttu-id="0b5b8-123">範例用法</span><span class="sxs-lookup"><span data-stu-id="0b5b8-123">Sample usage</span></span> |
|--------|---------------|
| <span data-ttu-id="0b5b8-124">建立</span><span class="sxs-lookup"><span data-stu-id="0b5b8-124">Create</span></span> | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| <span data-ttu-id="0b5b8-125">套用</span><span class="sxs-lookup"><span data-stu-id="0b5b8-125">Apply</span></span>  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| <span data-ttu-id="0b5b8-126">刪除</span><span class="sxs-lookup"><span data-stu-id="0b5b8-126">Delete</span></span> | `azure.Disks.DeleteById(id)` | 
| <span data-ttu-id="0b5b8-127">列出</span><span class="sxs-lookup"><span data-stu-id="0b5b8-127">List</span></span>   | `azure.SqlServers.List()` | 
| <span data-ttu-id="0b5b8-128">取得</span><span class="sxs-lookup"><span data-stu-id="0b5b8-128">Get</span></span>    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="0b5b8-129">`Define()` 和 `Update()` 是動詞，但除非後面接著 `Create()` 或 `Apply()`，否則不會封鎖。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-129">`Define()` and `Update()` are verbs but do not block unless followed by a `Create()` or `Apply()`.</span></span>
 
<span data-ttu-id="0b5b8-130">特定資源物件具有動詞，從而會在 Azure 中變更資源的狀態。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-130">Specific resource objects have verbs that change the state of the resource in Azure.</span></span> <span data-ttu-id="0b5b8-131">例如︰</span><span class="sxs-lookup"><span data-stu-id="0b5b8-131">For example:</span></span>

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

<span data-ttu-id="0b5b8-132">本節中所述的大部分方法也有非同步版本，以後置詞 `Async` 來表示。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-132">Most of the methods described in this section have an asynchronous version as well, denoted by the suffix `Async`.</span></span>

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a><span data-ttu-id="0b5b8-133">資源建立緩慢</span><span class="sxs-lookup"><span data-stu-id="0b5b8-133">Lazy resource creation</span></span>

<span data-ttu-id="0b5b8-134">在建立 Azure 資源時，如果新的資源需要仰賴另一項尚不存在的資源時，就會引發一項挑戰。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-134">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="0b5b8-135">我們以「在建立新的虛擬機器時保留公用 IP 位址並設定磁碟」為例。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-135">An example is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="0b5b8-136">您不需要確認是否保留位址或建立磁碟，只需要使用這些資源來設定虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-136">You don't want to verify reserving the address or the creating the disk, you just want to configure the virtual machine with those resources.</span></span>

<span data-ttu-id="0b5b8-137">請使用可建立的物件來定義要在程式碼中使用的 Azure 資源，但只在 Azure 中需要時才建立。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-137">Use creatable objects to define Azure resources for use in your code but only create them when needed in Azure.</span></span> <span data-ttu-id="0b5b8-138">使用可建立的物件撰寫之程式碼會將 Azure 環境中的資源建立卸載至管理 API，從而提升效能。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-138">Code written with creatable objects offloads resource creation in the Azure environment to the management API, boosting performance.</span></span> 

<span data-ttu-id="0b5b8-139">透過資源集合的 `Define()` 動詞而不含 `Create()` 動詞來產生可建立的物件：</span><span class="sxs-lookup"><span data-stu-id="0b5b8-139">Generate creatable objects through the resource collections' `Define()` verb without a `Create()` verb:</span></span>

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

<span data-ttu-id="0b5b8-140">由可建立之物件所定義的 Azure 資源尚未存在於訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-140">The Azure resource defined by the creatable object does not yet exist in your subscription.</span></span> <span data-ttu-id="0b5b8-141">可建立的物件是資源的本機表示法，管理 API 會視需要加以建立 (當呼叫 `.Create()` 時)。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-141">A creatable object is a local representation of a resource that the management API will create when it's needed (when `.Create()` is called).</span></span> <span data-ttu-id="0b5b8-142">在需要此資源的其他 Azure 資源之定義中使用這個可建立的物件。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-142">Use this creatable object in the definition of other Azure resources that need this resource.</span></span> 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

<span data-ttu-id="0b5b8-143">使用資源集合的 `Create()` 方法，在 Azure 訂用帳戶中建立資源。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-143">Create the resources in your Azure subscription using the `Create()` method for the resource collection.</span></span> 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

<span data-ttu-id="0b5b8-144">將可建立的物件傳遞至 `Create()` 會傳回 `ICreatedResources` 物件，而非傳回單一資源物件。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-144">Passing creatable objects to `Create()` returns a `ICreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="0b5b8-145">`CreatedRelatedResource` 物件可讓您存取 `Create()` 呼叫所建立的所有資源，而不只是資源集合的類型。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-145">The `CreatedRelatedResource` object lets you access all resources created by the `Create()` call, not just the type from the resource collection.</span></span> <span data-ttu-id="0b5b8-146">若要存取在 Azure 中為上述範例所建立之虛擬機器而建立的公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="0b5b8-146">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a><span data-ttu-id="0b5b8-147">例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="0b5b8-147">Exception handling</span></span>

<span data-ttu-id="0b5b8-148">管理 API 會定義延伸 `Microsoft.Rest.RestException` 的例外狀況類別。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-148">The management API defines exception classes that extend `Microsoft.Rest.RestException`.</span></span> <span data-ttu-id="0b5b8-149">在相關的 `try` 陳述式之後加上 `catch (RestException exception)` 區塊，即可攔截管理 API 所產生的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-149">Catch exceptions generated by management API, with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-tracing"></a><span data-ttu-id="0b5b8-150">記錄和追蹤</span><span class="sxs-lookup"><span data-stu-id="0b5b8-150">Logs and tracing</span></span>

<span data-ttu-id="0b5b8-151">適用於 .NET 的 Fluent Azure 管理程式庫中的記錄會運用基礎 [AutoRest](https://github.com/Azure/AutoRest) 服務用戶端追蹤。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-151">Logging in the fluent Azure management libraries for .NET leverages the underlying [AutoRest](https://github.com/Azure/AutoRest) service client tracing.</span></span>

<span data-ttu-id="0b5b8-152">建立會實作 `Microsoft.Rest.IServiceClientTracingInterceptor` 的類別。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-152">Create a class that implements `Microsoft.Rest.IServiceClientTracingInterceptor`.</span></span>  <span data-ttu-id="0b5b8-153">這個類別會負責攔截記錄訊息，並將它們傳遞至您在使用的任何記錄機制。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-153">This class will be responsible for intercepting log messages and passing them to whatever logging mechanism you're using.</span></span>  <span data-ttu-id="0b5b8-154">在此範例中，我們只要撰寫訊息至主控台，但您也可以將它們傳遞給 Log4Net、`Microsoft.Extensions.Logging`，或任何其他記錄架構。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-154">In this example, we're just writing messages to the console, but you could also pass them to Log4Net, `Microsoft.Extensions.Logging`, or any other logging framework.</span></span>

```csharp
class ConsoleTracer : IServiceClientTracingInterceptor
{
    public void Information(string message)
    {
        Console.WriteLine(message);
    }

    public void TraceError(string invocationId, Exception exception)
    {
        Console.WriteLine("Exception in {0}: {1}", invocationId, exception);
    }

    public void ReceiveResponse(string invocationId, HttpResponseMessage response) { }

    public void SendRequest(string invocationId, HttpRequestMessage request) { }

    public void Configuration(string source, string name, string value) { }

    public void EnterMethod(string invocationId, object instance, string method, IDictionary<string, object> parameters) { }

    public void ExitMethod(string invocationId, object returnValue) { }
}
```

<span data-ttu-id="0b5b8-155">建立 `Microsoft.Azure.Management.Fluent.Azure` 物件之前，請呼叫 `ServiceClientTracing.AddTracingInterceptor()` 並將 `ServiceClientTracing.IsEnabled` 設定為 *true*，將上面建立的 `IServiceClientTracingInterceptor` 初始化。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-155">Before creating the `Microsoft.Azure.Management.Fluent.Azure` object, initialize the `IServiceClientTracingInterceptor` you created above by calling `ServiceClientTracing.AddTracingInterceptor()` and set `ServiceClientTracing.IsEnabled` to *true*.</span></span>  <span data-ttu-id="0b5b8-156">當您建立 `Azure` 物件時，包含 `.WithDelegatingHandler()` 和 `.WithLogLevel()` 方法，將用戶端連接到 AutoRest 的服務用戶端追蹤。</span><span class="sxs-lookup"><span data-stu-id="0b5b8-156">When you create the `Azure` object, include the `.WithDelegatingHandler()` and `.WithLogLevel()` methods to wire up the client to AutoRest's service client tracing.</span></span>

```csharp
ServiceClientTracing.AddTracingInterceptor(new ConsoleTracer());
ServiceClientTracing.IsEnabled = true;

var azure = Azure
    .Configure()
    .WithDelegatingHandler(new HttpLoggingDelegatingHandler())
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

<span data-ttu-id="0b5b8-157">`HttpLoggingDelegatingHandler` 記錄層級定義如下：</span><span class="sxs-lookup"><span data-stu-id="0b5b8-157">The `HttpLoggingDelegatingHandler` log levels are defined as follows:</span></span>

| <span data-ttu-id="0b5b8-158">追蹤層級</span><span class="sxs-lookup"><span data-stu-id="0b5b8-158">Trace level</span></span> | <span data-ttu-id="0b5b8-159">啟用記錄</span><span class="sxs-lookup"><span data-stu-id="0b5b8-159">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="0b5b8-160">HttpLoggingDelegatingHandler.Level.None</span><span class="sxs-lookup"><span data-stu-id="0b5b8-160">HttpLoggingDelegatingHandler.Level.None</span></span> | <span data-ttu-id="0b5b8-161">沒有輸出</span><span class="sxs-lookup"><span data-stu-id="0b5b8-161">No output</span></span>
| <span data-ttu-id="0b5b8-162">HttpLoggingDelegatingHandler.Level.Basic</span><span class="sxs-lookup"><span data-stu-id="0b5b8-162">HttpLoggingDelegatingHandler.Level.Basic</span></span> | <span data-ttu-id="0b5b8-163">記錄基礎 REST 呼叫的 URL、回應碼和時間</span><span class="sxs-lookup"><span data-stu-id="0b5b8-163">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="0b5b8-164">HttpLoggingDelegatingHandler.Level.Body</span><span class="sxs-lookup"><span data-stu-id="0b5b8-164">HttpLoggingDelegatingHandler.Level.Body</span></span> | <span data-ttu-id="0b5b8-165">Basic 中的所有項目，以及 REST 呼叫的要求和回應內文</span><span class="sxs-lookup"><span data-stu-id="0b5b8-165">Everything in Basic plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="0b5b8-166">HttpLoggingDelegatingHandler.Level.Headers</span><span class="sxs-lookup"><span data-stu-id="0b5b8-166">HttpLoggingDelegatingHandler.Level.Headers</span></span> | <span data-ttu-id="0b5b8-167">Basic 中的所有項目，以及 REST 呼叫的要求和回應標頭</span><span class="sxs-lookup"><span data-stu-id="0b5b8-167">Everything in Basic plus the request and response headers REST calls</span></span>
| <span data-ttu-id="0b5b8-168">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span><span class="sxs-lookup"><span data-stu-id="0b5b8-168">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span></span> | <span data-ttu-id="0b5b8-169">Body 中的所有項目，以及 Headers 記錄層級</span><span class="sxs-lookup"><span data-stu-id="0b5b8-169">Everything in both Body and Headers log level</span></span>
