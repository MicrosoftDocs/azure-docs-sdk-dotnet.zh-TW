---
title: "適用於 Azure 開發人員的 .NET"
description: "適用於 Azure 開發人員的 .NET"
keywords: "Azure .NET, SDK, Azure .NET API 參考, Azure .NET 類別庫"
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.assetid: 
ms.openlocfilehash: eb7aa364cae9deea4ed2052eefdbd51c85379afa
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/26/2017
---
# <a name="get-started-with-net-for-azure-developers"></a>適用於 Azure 開發人員的 .NET 快速入門

本教學課程將逐步引導您使用 Visual Studio 和 .NET 來建置及部署 Microsoft Azure 應用程式。  完成時，您會在 ASP.NET MVC Core 中建置載作為 Azure Web 應用程式的 Web 架構待辦事項應用程式，並將 Azure CosmosDB 用於資料儲存體。

## <a name="prerequisites"></a>必要條件

* [Visual Studio 2017](https://www.visualstudio.com/downloads/)
* [Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/)

## <a name="create-a-cosmosdb-account"></a>建立 CosmosDB 帳戶

本教學課程中的資料儲存體將需要用到 CosmosDB，因此您必須建立帳戶。  在本機或 Cloud Shell 中執行這個指令碼，可建立 Azure CosmosDB DocumentDB API 帳戶。  按一下下方程式碼區塊上的 [試試看]按鈕以啟動 [Azure Cloud Shell](/azure/cloud-shell/)，並將指令碼區塊複製/貼上殼層。

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the CosmosDB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

請記下顯示的 **authKey** 和**端點** 

## <a name="downloading-and-running-the-application"></a>下載和執行應用程式

讓我們來取得這個逐步解說的範例程式碼，並將其連線到您的 CosmosDB 帳戶。

1. 下載範例程式碼。  您可以[從 GitHub 取得](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)，或如果您有 [Git 命令列用戶端](https://git-scm.com/)，則使用下列命令將其複製到本機電腦：

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. 在 Visual Studio 中開啟 **todo.csproj**。

3. 在 Web 專案中開啟 **appsettings.json**。  尋找下列幾行︰

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    使用您先前記下的值取代 **AUTHKEYVALUE** 和 **ENDPOINTVALUE**。

4. 按一下 **F5** 還原專案的 NuGet 套件，建置專案，並在本機執行。

Web 應用程式應會在您的本機瀏覽器中執行。  按一下 [新建] 即可將新項目新增至待辦事項清單。  請注意您在應用程式中輸入的資料會儲存至 CosmosDB 帳戶。  您可以[在 Azure 入口網站中檢視您的資料](/azure/documentdb/documentdb-view-json-document-explorer)。

## <a name="deploying-the-application-as-an-azure-web-app"></a>將 Web 應用程式部署為 Azure Web 應用程式

您已成功建置使用 DocumentDB 等 Azure 服務的應用程式。  接下來，我們會將 Web 應用程式部署至雲端。

> [!IMPORTANT]
> 請務必使用與您的 Azure 訂用帳戶相關聯的相同帳戶登入 Visual Studio。

1. 在 Visual Studio 方案總管中，以滑鼠右鍵按一下專案名稱，並選取 [發行...]

2. 使用 [發佈] 對話方塊，選取 [Microsoft Azure App Service]，選取 [新建]，然後按一下 [發佈]

3. 完成 [建立 App Service] 對話方塊，如下所示：

    * 輸入唯一 **Web 應用程式名稱**。  這會是應用程式 URL 的一部分。
    * 選取您正在部署的 Azure **訂用帳戶**。  使用與您稍早已登入 Cloud Shell 相同的訂用帳戶。
    * 選取 Web 應用程式**資源群組**的 [DotNetAzureTutorial] 。
    * 選取或建立 **App Service 方案**來決定您應用程式的定價。  這裡有[更多關於 App Service 方案的資訊](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)。

4. 按一下 [建立] 以部署應用程式。  部署完成時，瀏覽器會開啟已部署的應用程式。

![已完成的應用程式](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>清除

當您完成測試應用程式及檢查程式碼和資源時，可以透過刪除資源群組，將 Web 應用程式和 CosmosDB 帳戶刪除。 在 Cloud Shell 中。

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>後續步驟

* [在 ASP.NET Web 應用程式中使用驗證的 Azure Active Directory](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [使用 Azure SQL Database 來建置 Azure Web 應用程式](/azure/app-service-web/web-sites-dotnet-get-started)
* [使用 Azure 儲存體嘗試 .NET 範例應用程式](/azure/storage/storage-samples-dotnet)


