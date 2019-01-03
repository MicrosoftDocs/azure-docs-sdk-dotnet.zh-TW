---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 5c8cb328802cfb94e944e4241852fb9568e8507f
ms.sourcegitcommit: e25b6ac74033f3b0a7610bf66feb654acb43054c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53430511"
---
.NET 應用程式需要您 Azure 訂用帳戶的讀取和建立資源權限，才能使用適用於 .NET 的 Azure 管理程式庫。 請建立服務主體，並將應用程式設定為使用其認證來授予此存取權。 服務主體可讓您建立與身分識別相關聯的非互動式帳戶，而且對於此身分識別，您只賦予它應用程式執行時所需的權限。

首先，請登入 [Azure Cloud Shell](https://shell.azure.com/bash)。 確認您目前使用的訂用帳戶，是您希望建立服務主體的位置。 

```azurecli-interactive
az account show
```

系統會顯示您的訂用帳戶資訊。

```json
{
  "environmentName": "AzureCloud",
  "id": "15dbcfa8-4b93-4c9a-881c-6189d39f04d4",
  "isDefault": true,
  "name": "my-subscription",
  "state": "Enabled",
  "tenantId": "43413cc1-5886-4711-9804-8cfea3d1c3ee",
  "user": {
    "cloudShellID": true,
    "name": "jane@contoso.com",
    "type": "user"
  }
}
```

如果您並未登入正確的訂用帳戶，請輸入 `az account set -s <name or ID of subscription>`，以選取正確的訂用帳戶。

使用下列命令建立服務主體：

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

服務主體資訊會顯示為 JSON。

```json
{
  "clientId": "b52dd125-9272-4b21-9862-0be667bdf6dc",
  "clientSecret": "ebc6e170-72b2-4b6f-9de2-99410964d2d0",
  "subscriptionId": "ffa52f27-be12-4cad-b1ea-c2c241b6cceb",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

複製 JSON 輸出，並貼到文字編輯器中供稍後使用。
