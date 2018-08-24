建立名為 `azureauth.json` 的文字檔。 從您已建立的服務主體處將 JSON 輸出貼上。

將此檔案儲存在系統上可供程式碼讀取且安全的位置。 使用 PowerShell 並使用檔案完整路徑來設定名為 `AZURE_AUTH_LOCATION` 的環境變數，例如：

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
