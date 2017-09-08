使用服務主體認證建立名為 `azureauth.properties` 的文字檔：

```plaintext
# sample management library properties file
subscription=15dbcfa8-4b93-4c9a-881c-6189d39f04d4
client=a2ab11af-01aa-4759-8345-7803287dbd39
key=password
tenant=43413cc1-5886-4711-9804-8cfea3d1c3ee
managementURI=https://management.core.windows.net/
baseURL=https://management.azure.com/
authURL=https://login.windows.net/
graphURL=https://graph.windows.net/
```

- subscription：執行 `Login-AzureRmAccount` 時，使用 SubscriptionId 值。
- client：使用從服務主體輸出所得到的 ApplicationId 值。
- key：執行 `New-AzureRmADServicePrincipal`時，使用您指派的 -Password 參數 (不含引號)。
- tenant：執行 `Login-AzureRmAccount`時，使用 TenantId 值。

將此檔案儲存在系統上可供程式碼讀取且安全的位置。 使用 PowerShell 並使用檔案完整路徑來設定名為 `AZURE_AUTH_LOCATION` 的環境變數，例如：

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
