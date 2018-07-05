<span data-ttu-id="34167-101">.NET 應用程式需要您 Azure 訂用帳戶的讀取和建立資源權限，才能使用適用於 .NET 的 Azure 管理程式庫。</span><span class="sxs-lookup"><span data-stu-id="34167-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="34167-102">請建立服務主體，並將應用程式設定為使用其認證來授予此存取權。</span><span class="sxs-lookup"><span data-stu-id="34167-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="34167-103">服務主體可讓您建立與身分識別相關聯的非互動式帳戶，而且對於此身分識別，您只賦予它應用程式執行時所需的權限。</span><span class="sxs-lookup"><span data-stu-id="34167-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="34167-104">首先，請登入 Azure PowerShell：</span><span class="sxs-lookup"><span data-stu-id="34167-104">First, login to Azure PowerShell:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="34167-105">請注意顯示您租用戶和訂用帳戶的資訊：</span><span class="sxs-lookup"><span data-stu-id="34167-105">Note the information displayed about your tenant and subscription:</span></span>

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

<span data-ttu-id="34167-106">[使用 PowerShell 建立服務主體](/powershell/azure/create-azure-service-principal-azureps)，如下所示。</span><span class="sxs-lookup"><span data-stu-id="34167-106">[Create a service principal using PowerShell](/powershell/azure/create-azure-service-principal-azureps) as shown below.</span></span> 

> [!NOTE]
> <span data-ttu-id="34167-107">若以下 `New-AzureRmADServicePrincipal` Cmdlet 傳回「其他具備相同值的 identifierUris 屬性物件已存在」，則表示您的租用戶中已經有該名稱的服務主體。</span><span class="sxs-lookup"><span data-stu-id="34167-107">If the `New-AzureRmADServicePrincipal` cmdlet below returns "Another object with the same value for property identifierUris already exists," there is already a service principal by that name in your tenant.</span></span> <span data-ttu-id="34167-108">針對 **DisplayName** 參數使用不同的值。</span><span class="sxs-lookup"><span data-stu-id="34167-108">Use a different value for the **DisplayName** parameter.</span></span> 

```powershell
# Create the service principal (use a strong password)
$cred = Get-Credential
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password $cred.Password

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

<span data-ttu-id="34167-109">請務必記下 ApplicationId：</span><span class="sxs-lookup"><span data-stu-id="34167-109">Make sure to note the ApplicationId:</span></span>

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
