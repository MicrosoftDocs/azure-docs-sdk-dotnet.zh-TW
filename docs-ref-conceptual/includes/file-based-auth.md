<span data-ttu-id="a6601-101">使用服務主體認證建立名為 `azureauth.properties` 的文字檔：</span><span class="sxs-lookup"><span data-stu-id="a6601-101">Create a text file named `azureauth.properties` using the service principal credentials:</span></span>

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

- <span data-ttu-id="a6601-102">subscription：執行 `Login-AzureRmAccount` 時，使用 SubscriptionId 值。</span><span class="sxs-lookup"><span data-stu-id="a6601-102">subscription: use the *SubscriptionId* value from when you ran `Login-AzureRmAccount`.</span></span>
- <span data-ttu-id="a6601-103">client：使用從服務主體輸出所得到的 ApplicationId 值。</span><span class="sxs-lookup"><span data-stu-id="a6601-103">client: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="a6601-104">key：執行 `New-AzureRmADServicePrincipal`時，使用您指派的 -Password 參數 (不含引號)。</span><span class="sxs-lookup"><span data-stu-id="a6601-104">key: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="a6601-105">tenant：執行 `Login-AzureRmAccount`時，使用 TenantId 值。</span><span class="sxs-lookup"><span data-stu-id="a6601-105">tenant: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="a6601-106">將此檔案儲存在系統上可供程式碼讀取且安全的位置。</span><span class="sxs-lookup"><span data-stu-id="a6601-106">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="a6601-107">使用 PowerShell 並使用檔案完整路徑來設定名為 `AZURE_AUTH_LOCATION` 的環境變數，例如：</span><span class="sxs-lookup"><span data-stu-id="a6601-107">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
