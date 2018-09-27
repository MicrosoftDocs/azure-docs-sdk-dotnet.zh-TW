---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190711"
---
建立名為 `azureauth.json` 的文字檔。 從您已建立的服務主體處將 JSON 輸出貼上。

將此檔案儲存在系統上可供程式碼讀取且安全的位置。 使用 PowerShell 並使用檔案完整路徑來設定名為 `AZURE_AUTH_LOCATION` 的環境變數，例如：

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
