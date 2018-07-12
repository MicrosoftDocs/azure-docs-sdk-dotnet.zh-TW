---
title: 適用於 .NET 之 Azure 管理程式庫的使用概念和模式
description: ''
keywords: Azure, .NET, SDK, API, 模式, 概念, Fluent, 記錄
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: b817216e114e5ab3ff22c1c5adb0f892c7874147
ms.sourcegitcommit: 1c2e1fd031ad012d6888fcde3cd325f7e8e49e0f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2018
ms.locfileid: "29752860"
---
# <a name="azure-management-library-for-net-fluent-concepts"></a>適用於 .NET Fluent 概念的 Azure 管理程式庫

本文將協助您了解如何有效地在適用於 .NET 的 Azure 管理程式庫中使用 Fluent 介面。

## <a name="building-resources-using-a-fluent-interface"></a>使用 Fluent 介面建置資源

Fluent 介面是建置者模式的特定表單，會透過強制執行正確資源設定的方法鏈結來建立物件。 例如，會使用 Fluent 介面來建立進入點 Azure 物件：

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a>資源集合

上面顯示的 `Microsoft.Azure.Management.Fluent.Azure` 物件是 Fluent 管理程式庫中所有資源建立的進入點。 請使用 `Azure` 物件中的資源集合來選取要處理哪種類型的資源。 例如，SQL Database：

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

如上所示，您與 API 的大部分 Fluent「對話」開頭都會選取您所需 Azure 資源的適當資源集合。  接著，Visual Studio 中的 Intellisense 會引導您完成交談。 

![Intellisense 的 GIF 會在 Visual Studio 中進行 Fluent 對話](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a>清單和反覆項目

每個資源集合都會有 `List()` 方法，以便傳回該資源在您目前訂用帳戶中的每個執行個體。 例如，`Azure.SqlServers.List()` 會傳回訂用帳戶中的所有 SQL 伺服器。

使用 `ListByResourceGroup()` 方法可將傳回的清單侷限在特定的 [Azure 資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)。  

請依照您對一般 `List<T>` 所進行的操作方式，來對傳回集合進行反覆執行：

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a>可採取動作的動詞

其名稱中有動詞命令的資源集合方法會在 Azure 中立即採取動作。 這些方法會同步運作，而且在完成之前會封鎖目前執行緒的執行。 

| 指令動詞   |  範例用法 |
|--------|---------------|
| 建立 | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| 套用  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| 刪除 | `azure.Disks.DeleteById(id)` | 
| 列出   | `azure.SqlServers.List()` | 
| 取得    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> `Define()` 和 `Update()` 是動詞，但除非後面接著 `Create()` 或 `Apply()`，否則不會封鎖。
 
特定資源物件具有動詞，從而會在 Azure 中變更資源的狀態。 例如︰

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

本節中所述的大部分方法也有非同步版本，以後置詞 `Async` 來表示。

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a>資源建立緩慢

在建立 Azure 資源時，如果新的資源需要仰賴另一項尚不存在的資源時，就會引發一項挑戰。 我們以「在建立新的虛擬機器時保留公用 IP 位址並設定磁碟」為例。 您不需要確認是否保留位址或建立磁碟，只需要使用這些資源來設定虛擬機器。

請使用可建立的物件來定義要在程式碼中使用的 Azure 資源，但只在 Azure 中需要時才建立。 使用可建立的物件撰寫之程式碼會將 Azure 環境中的資源建立卸載至管理 API，從而提升效能。 

透過資源集合的 `Define()` 動詞而不含 `Create()` 動詞來產生可建立的物件：

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

由可建立之物件所定義的 Azure 資源尚未存在於訂用帳戶中。 可建立的物件是資源的本機表示法，管理 API 會視需要加以建立 (當呼叫 `.Create()` 時)。 在需要此資源的其他 Azure 資源之定義中使用這個可建立的物件。 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

使用資源集合的 `Create()` 方法，在 Azure 訂用帳戶中建立資源。 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

將可建立的物件傳遞至 `Create()` 會傳回 `ICreatedResources` 物件，而非傳回單一資源物件。  `CreatedRelatedResource` 物件可讓您存取 `Create()` 呼叫所建立的所有資源，而不只是資源集合的類型。 若要存取在 Azure 中為上述範例所建立之虛擬機器而建立的公用 IP 位址：

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a>例外狀況處理

管理 API 會定義延伸 `Microsoft.Rest.RestException` 的例外狀況類別。 在相關的 `try` 陳述式之後加上 `catch (RestException exception)` 區塊，即可攔截管理 API 所產生的例外狀況。

## <a name="logs-and-tracing"></a>記錄和追蹤

適用於 .NET 的 Fluent Azure 管理程式庫中的記錄會運用基礎 [AutoRest](https://github.com/Azure/AutoRest) 服務用戶端追蹤。

建立會實作 `Microsoft.Rest.IServiceClientTracingInterceptor` 的類別。  這個類別會負責攔截記錄訊息，並將它們傳遞至您在使用的任何記錄機制。  在此範例中，我們只要撰寫訊息至主控台，但您也可以將它們傳遞給 Log4Net、`Microsoft.Extensions.Logging`，或任何其他記錄架構。

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

建立 `Microsoft.Azure.Management.Fluent.Azure` 物件之前，請呼叫 `ServiceClientTracing.AddTracingInterceptor()` 並將 `ServiceClientTracing.IsEnabled` 設定為 *true*，將上面建立的 `IServiceClientTracingInterceptor` 初始化。  當您建立 `Azure` 物件時，包含 `.WithDelegatingHandler()` 和 `.WithLogLevel()` 方法，將用戶端連接到 AutoRest 的服務用戶端追蹤。

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

`HttpLoggingDelegatingHandler` 記錄層級定義如下：

| 追蹤層級 | 啟用記錄 
| ------------ | ---------------
| HttpLoggingDelegatingHandler.Level.None | 沒有輸出
| HttpLoggingDelegatingHandler.Level.Basic | 記錄基礎 REST 呼叫的 URL、回應碼和時間
| HttpLoggingDelegatingHandler.Level.Body | Basic 中的所有項目，以及 REST 呼叫的要求和回應內文
| HttpLoggingDelegatingHandler.Level.Headers | Basic 中的所有項目，以及 REST 呼叫的要求和回應標頭
| HttpLoggingDelegatingHandler.Level.BodyAndHeaders | Body 中的所有項目，以及 Headers 記錄層級
