.NET 應用程式需要您 Azure 訂用帳戶的讀取和建立資源權限，才能使用適用於 .NET 的 Azure 管理程式庫。 請建立服務主體，並將應用程式設定為使用其認證來授予此存取權。 服務主體可讓您建立與身分識別相關聯的非互動式帳戶，而且對於此身分識別，您只賦予它應用程式執行時所需的權限。

首先，請登入 Azure PowerShell：

```powershell
Login-AzureRmAccount
```

請注意顯示您租用戶和訂用帳戶的資訊：

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

[使用 PowerShell 建立服務主體](/powershell/azure/create-azure-service-principal-azureps)，如下所示。 

> [!NOTE]
> 若以下 `New-AzureRmADServicePrincipal` Cmdlet 傳回「其他具備相同值的 identifierUris 屬性物件已存在」，則表示您的租用戶中已經有該名稱的服務主體。 針對 **DisplayName** 參數使用不同的值。 

```powershell
# Create the service principal (use a strong password)
$cred = Get-Credential
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password $cred.Password

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

請務必記下 ApplicationId：

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
