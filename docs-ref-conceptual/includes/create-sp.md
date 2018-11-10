---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 5c8cb328802cfb94e944e4241852fb9568e8507f
ms.sourcegitcommit: 70982e900bd4adfbc121eba55d94544f17c6b495
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51196044"
---
<span data-ttu-id="977e5-101">.NET 應用程式需要您 Azure 訂用帳戶的讀取和建立資源權限，才能使用適用於 .NET 的 Azure 管理程式庫。</span><span class="sxs-lookup"><span data-stu-id="977e5-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="977e5-102">請建立服務主體，並將應用程式設定為使用其認證來授予此存取權。</span><span class="sxs-lookup"><span data-stu-id="977e5-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="977e5-103">服務主體可讓您建立與身分識別相關聯的非互動式帳戶，而且對於此身分識別，您只賦予它應用程式執行時所需的權限。</span><span class="sxs-lookup"><span data-stu-id="977e5-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="977e5-104">首先，請登入 [Azure Cloud Shell](https://shell.azure.com/bash)。</span><span class="sxs-lookup"><span data-stu-id="977e5-104">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="977e5-105">確認您目前使用的訂用帳戶，是您希望建立服務主體的位置。</span><span class="sxs-lookup"><span data-stu-id="977e5-105">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="977e5-106">系統會顯示您的訂用帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="977e5-106">Your subscription information is displayed.</span></span>

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

<span data-ttu-id="977e5-107">如果您並未登入正確的訂用帳戶，請輸入 `az account set -s <name or ID of subscription>`，以選取正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="977e5-107">If you're not logged into the correct subscription, select the correct one by typing `az account set -s <name or ID of subscription>`.</span></span>

<span data-ttu-id="977e5-108">使用下列命令建立服務主體：</span><span class="sxs-lookup"><span data-stu-id="977e5-108">Create the service principal with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

<span data-ttu-id="977e5-109">服務主體資訊會顯示為 JSON。</span><span class="sxs-lookup"><span data-stu-id="977e5-109">The service principal information is displayed as JSON.</span></span>

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

<span data-ttu-id="977e5-110">複製 JSON 輸出，並貼到文字編輯器中供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="977e5-110">Copy and paste the JSON output to a text editor for use later.</span></span>
