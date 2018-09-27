---
title: 使用 .NET Core 從命令列部署至 Azure
description: 本文說明如何使用命令列工具，將 ASP.NET Core 應用程式部署至 Azure App Service。
ms.date: 06/20/2017
ms.openlocfilehash: a29f5474dcfedc6f8d044f09ad4d54c5be6a371f
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190491"
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a>使用 .NET Core 從命令列部署至 Azure

本教學課程將逐步引導您使用 .NET Core 來建置及部署 Microsoft Azure 應用程式。  完成時，您會在 ASP.NET MVC Core 中建置裝載為 Azure Web 應用程式的 Web 架構待辦事項應用程式，並將 Azure Cosmos DB 用於資料儲存體。

## <a name="prerequisites"></a>必要條件

* [Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/)
* [.NET Core](https://www.microsoft.com/net/download/core) (選擇性)
* [Azure CLI 2.0](/cli/azure/install-az-cli2) (選擇性)
* [Git](https://www.git-scm.com/) 命令列用戶端 (選擇性)

[Azure Cloud Shell](/azure/cloud-shell/) 具有此預先安裝教學課程的所有選用必要條件。  如果您需要在本機執行本教學課程，只需要安裝上述的選用元件。  若要快速啟動 Cloud Shell，只要按一下任何程式碼區塊右上方的 [試試看] 按鈕即可。

## <a name="create-an-azure-cosmos-db-account"></a>建立 Azure Cosmos DB 帳戶

在此教學課程中，會將 Azure Cosmos DB 當做資料儲存體，因此您需要建立一個帳戶。  在本機或 Cloud Shell 中執行這個指令碼，以建立 Azure Cosmos DB SQL API 帳戶。

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the Azure Cosmos DB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)

```

## <a name="download-and-configure-the-application"></a>下載並設定應用程式

您要部署的應用程式是使用 Azure Cosmos DB 用戶端程式庫，透過 ASP.NET MVC Core 所撰寫的[簡單待辦事項應用程式](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)。  現在，您會取得此教學課程的程式碼，並使用您的 Azure Cosmos DB 資訊進行設定。

```azurecli-interactive
# Get the code from GitHub
git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart

# Change the working directory
cd dotnet-cosmosdb-quickstart

# Replace authKey and endpoint values in appsettings.json
sed -i "s|AUTHKEYVALUE|$cosmosAuthKey|g" appsettings.json
sed -i "s|ENDPOINTVALUE|$cosmosEndpoint|g" appsettings.json

# Now commit your changes to the local Git repository.
git commit -a -m "Modified settings"

```

> [!NOTE]
> 如果您從未在此環境中執行過 `git commit`，系統可能會提示您設定身分識別。 遵循螢幕上指示，然後重新執行 `git commit` 命令。

還原 NuGet 套件，並建置應用程式。

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> 如果您在自己電腦上使用工具，可以執行 `dotnet run` 並瀏覽至顯示的 `localhost` 位址來測試應用程式。  不過，您無法在 Cloud Shell 中瀏覽至此位址。  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a>設定 Azure App Service 及部署 web 應用程式

您已成功下載及建置 web 應用程式，並準備要將其部署為 Azure Web 應用程式。  您將先建立 Web 應用程式資源。

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

在部署之前，您必須設定帳戶層級的部署認證。  使用下列指令碼，確定包含您自己的使用者名稱和密碼值。

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

最後，將應用程式部署至 Azure。  系統會提示您輸入先前建立的密碼。

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

將會遠端建置和部署應用程式。  瀏覽至 `https://<web app name>.azurewebsites.net` 來測試應用程式。  若要在主控台中顯示位址，請使用下列方法：

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

按一下 [新建] 即可將新項目新增至待辦事項清單。

![已完成的應用程式](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>清除

當您完成應用程式測試及程式碼和資源的檢查時，可以透過刪除資源群組，將 Web 應用程式和 Azure Cosmos DB 帳戶刪除。

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>後續步驟

* [在 ASP.NET Web 應用程式中使用驗證的 Azure Active Directory](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [使用 Azure SQL Database 來建置 Azure Web 應用程式](/azure/app-service-web/web-sites-dotnet-get-started)
* [使用 Azure 儲存體嘗試 .NET 範例應用程式](/azure/storage/storage-samples-dotnet)


