<span data-ttu-id="cf44b-101">建立名為 `azureauth.json` 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="cf44b-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="cf44b-102">從您已建立的服務主體處將 JSON 輸出貼上。</span><span class="sxs-lookup"><span data-stu-id="cf44b-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="cf44b-103">將此檔案儲存在系統上可供程式碼讀取且安全的位置。</span><span class="sxs-lookup"><span data-stu-id="cf44b-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="cf44b-104">使用 PowerShell 並使用檔案完整路徑來設定名為 `AZURE_AUTH_LOCATION` 的環境變數，例如：</span><span class="sxs-lookup"><span data-stu-id="cf44b-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
