---
title: "使用 .NET Core 從命令列部署至 Azure"
description: "本文說明如何使用命令列工具，將 ASP.NET Core 應用程式部署至 Azure App Service。"
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
ms.openlocfilehash: 2ed69bfed7310c9e6b2f3f8fedb906ce33d87c3c
ms.sourcegitcommit: c630918c9e17f5e3c6d4f28fe740c041f60b1e66
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2017
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a><span data-ttu-id="88773-104">使用 .NET Core 從命令列部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="88773-104">Deploy to Azure from the command line with .NET Core</span></span>

<span data-ttu-id="88773-105">本教學課程將逐步引導您使用 .NET Core 來建置及部署 Microsoft Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88773-105">This tutorial will walk you through building and deploying a Microsoft Azure application using .NET Core.</span></span>  <span data-ttu-id="88773-106">完成時，您會在 ASP.NET MVC Core 中建置載作為 Azure Web 應用程式的 Web 架構待辦事項應用程式，並將 Azure CosmosDB 用於資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="88773-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure CosmosDB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88773-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="88773-107">Prerequisites</span></span>

* <span data-ttu-id="88773-108">[Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="88773-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="88773-109">[.NET Core](https://www.microsoft.com/net/download/core) (選擇性)</span><span class="sxs-lookup"><span data-stu-id="88773-109">[.NET Core](https://www.microsoft.com/net/download/core) (optional)</span></span>
* <span data-ttu-id="88773-110">[Azure CLI 2.0](/cli/azure/install-az-cli2) (選擇性)</span><span class="sxs-lookup"><span data-stu-id="88773-110">[Azure CLI 2.0](/cli/azure/install-az-cli2) (optional)</span></span>
* <span data-ttu-id="88773-111">[Git](https://www.git-scm.com/) 命令列用戶端 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="88773-111">[Git](https://www.git-scm.com/) command line client (optional)</span></span>

<span data-ttu-id="88773-112">[Azure Cloud Shell](/azure/cloud-shell/) 具有此預先安裝教學課程的所有選用必要條件。</span><span class="sxs-lookup"><span data-stu-id="88773-112">The [Azure Cloud Shell](/azure/cloud-shell/) has all of the optional prerequisites for this tutorial preinstalled.</span></span>  <span data-ttu-id="88773-113">如果您需要在本機執行本教學課程，只需要安裝上述的選用元件。</span><span class="sxs-lookup"><span data-stu-id="88773-113">You only need to install the optional components above if you wish to run the tutorial locally.</span></span>  <span data-ttu-id="88773-114">若要快速啟動 Cloud Shell，只要按一下任何程式碼區塊右上方的 [試試看] 按鈕即可。</span><span class="sxs-lookup"><span data-stu-id="88773-114">To quickly launch the Cloud Shell, just click the **Try it** button in the top-right of any of the below code blocks.</span></span>

## <a name="create-a-cosmosdb-account"></a><span data-ttu-id="88773-115">建立 CosmosDB 帳戶</span><span class="sxs-lookup"><span data-stu-id="88773-115">Create a CosmosDB account</span></span>

<span data-ttu-id="88773-116">本教學課程中的資料儲存體將需要用到 CosmosDB，因此您必須建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="88773-116">CosmosDB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="88773-117">在本機或 Cloud Shell 中執行這個指令碼，可建立 Azure CosmosDB DocumentDB API 帳戶。</span><span class="sxs-lookup"><span data-stu-id="88773-117">Run this script locally or in the Cloud Shell to create an Azure CosmosDB DocumentDB API account.</span></span>

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

```

## <a name="download-and-configure-the-application"></a><span data-ttu-id="88773-118">下載並設定應用程式</span><span class="sxs-lookup"><span data-stu-id="88773-118">Download and configure the application</span></span>

<span data-ttu-id="88773-119">您要部署的應用程式是使用 CosmosDB 用戶端程式庫，透過 ASP.NET MVC Core 所撰寫的[簡單待辦事項應用程式](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)。</span><span class="sxs-lookup"><span data-stu-id="88773-119">The application you're going to deploy is a [simple to-do app](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) written using ASP.NET MVC Core using the CosmosDB client libraries.</span></span>  <span data-ttu-id="88773-120">現在，您會取得此教學課程的程式碼，並使用您的 CosmosDB 資訊進行設定。</span><span class="sxs-lookup"><span data-stu-id="88773-120">Now you'll get the code for this tutorial and configure it with your CosmosDB information.</span></span>

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
> <span data-ttu-id="88773-121">如果您從未在此環境中執行過 `git commit`，系統可能會提示您設定身分識別。</span><span class="sxs-lookup"><span data-stu-id="88773-121">If you've never run `git commit` in this environment before, you may be prompted to set your identity.</span></span> <span data-ttu-id="88773-122">遵循螢幕上指示，然後重新執行 `git commit` 命令。</span><span class="sxs-lookup"><span data-stu-id="88773-122">Follow the on-screen instructions and then re-run the `git commit` command.</span></span>

<span data-ttu-id="88773-123">還原 NuGet 套件，並建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="88773-123">Restore the NuGet packages and build the application.</span></span>

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> <span data-ttu-id="88773-124">如果您在自己電腦上使用工具，可以執行 `dotnet run` 並瀏覽至顯示的 `localhost` 位址來測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="88773-124">If you are using the tools on your own machine, you can test the application by running `dotnet run` and browsing to the displayed `localhost` address.</span></span>  <span data-ttu-id="88773-125">不過，您無法在 Cloud Shell 中瀏覽至此位址。</span><span class="sxs-lookup"><span data-stu-id="88773-125">You are not able to browse to this address in the Cloud Shell, however.</span></span>  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a><span data-ttu-id="88773-126">設定 Azure App Service 及部署 web 應用程式</span><span class="sxs-lookup"><span data-stu-id="88773-126">Configure Azure App Service and deploy the web app</span></span>

<span data-ttu-id="88773-127">您已成功下載及建置 web 應用程式，並準備要將其部署為 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="88773-127">You've successfully downloaded and built the web application, and you're ready to deploy it as an Azure Web App.</span></span>  <span data-ttu-id="88773-128">您將先建立 Web 應用程式資源。</span><span class="sxs-lookup"><span data-stu-id="88773-128">You'll start by creating the Web App resource.</span></span>

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

<span data-ttu-id="88773-129">在部署之前，您必須設定帳戶層級的部署認證。</span><span class="sxs-lookup"><span data-stu-id="88773-129">Before you deploy, you need to set the account-level deployment credentials.</span></span>  <span data-ttu-id="88773-130">使用下列指令碼，確定包含您自己的使用者名稱和密碼值。</span><span class="sxs-lookup"><span data-stu-id="88773-130">Use the script below, making sure to include your own values for the user name and password.</span></span>

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

<span data-ttu-id="88773-131">最後，將應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="88773-131">Finally, deploy the application to Azure.</span></span>  <span data-ttu-id="88773-132">系統會提示您輸入先前建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="88773-132">You will be prompted for the password you created above.</span></span>

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

<span data-ttu-id="88773-133">將會遠端建置和部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="88773-133">The application will be built remotely and deployed.</span></span>  <span data-ttu-id="88773-134">瀏覽至 `https://<web app name>.azurewebsites.net` 來測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="88773-134">Test the application by browsing to `https://<web app name>.azurewebsites.net`.</span></span>  <span data-ttu-id="88773-135">若要在主控台中顯示位址，請使用下列方法：</span><span class="sxs-lookup"><span data-stu-id="88773-135">To display the address in the console, use the following:</span></span>

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

<span data-ttu-id="88773-136">您可以將新項目新增至待辦事項清單，方法是按一下 [新建]。</span><span class="sxs-lookup"><span data-stu-id="88773-136">You can add new items to the to-do list by clicking **Create New**.</span></span>

![已完成的應用程式](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="88773-138">清除</span><span class="sxs-lookup"><span data-stu-id="88773-138">Clean up</span></span>

<span data-ttu-id="88773-139">當您完成測試應用程式及檢查程式碼和資源時，可以透過刪除資源群組，將 Web 應用程式和 CosmosDB 帳戶刪除。</span><span class="sxs-lookup"><span data-stu-id="88773-139">When you're done testing the app and inspecting the code and resources, you can delete the Web App and CosmosDB account by deleting the resource group.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="88773-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="88773-140">Next steps</span></span>

* [<span data-ttu-id="88773-141">在 ASP.NET Web 應用程式中使用驗證的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="88773-141">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="88773-142">使用 Azure SQL Database 來建置 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="88773-142">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="88773-143">使用 Azure 儲存體嘗試 .NET 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="88773-143">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


