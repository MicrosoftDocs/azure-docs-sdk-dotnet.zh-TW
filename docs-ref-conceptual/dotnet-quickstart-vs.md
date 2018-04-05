---
title: 從 Visual Studio 部署至 Azure
description: 本教學課程將逐步引導您使用 Visual Studio 和 .NET 來建置及部署 Microsoft Azure 應用程式。
keywords: Azure .NET, SDK, Azure .NET API 參考, Azure .NET 類別庫
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: d5c34dfc7e649e00e8ef458537f3f76410db61d4
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/05/2018
---
# <a name="deploy-to-azure-from-visual-studio"></a><span data-ttu-id="8fd43-104">從 Visual Studio 部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="8fd43-104">Deploy to Azure from Visual Studio</span></span>

<span data-ttu-id="8fd43-105">本教學課程將逐步引導您使用 Visual Studio 和 .NET 來建置及部署 Microsoft Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8fd43-105">This tutorial will walk you through building and deploying a Microsoft Azure application using Visual Studio and .NET.</span></span>  <span data-ttu-id="8fd43-106">完成時，您會在 ASP.NET MVC Core 中建置載作為 Azure Web 應用程式的 Web 架構待辦事項應用程式，並將 Azure CosmosDB 用於資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="8fd43-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure CosmosDB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fd43-107">先決條件</span><span class="sxs-lookup"><span data-stu-id="8fd43-107">Prerequisites</span></span>

* [<span data-ttu-id="8fd43-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8fd43-108">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="8fd43-109">[Microsoft Azure 訂用帳戶](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="8fd43-109">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>

## <a name="create-a-cosmosdb-account"></a><span data-ttu-id="8fd43-110">建立 CosmosDB 帳戶</span><span class="sxs-lookup"><span data-stu-id="8fd43-110">Create a CosmosDB account</span></span>

<span data-ttu-id="8fd43-111">本教學課程中的資料儲存體將需要用到 CosmosDB，因此您必須建立帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fd43-111">CosmosDB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="8fd43-112">在本機或 Cloud Shell 中執行這個指令碼，可建立 Azure CosmosDB DocumentDB API 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fd43-112">Run this script locally or in the Cloud Shell to create an Azure CosmosDB DocumentDB API account.</span></span>  <span data-ttu-id="8fd43-113">按一下下方程式碼區塊上的 [試試看]按鈕以啟動 [Azure Cloud Shell](/azure/cloud-shell/)，並將指令碼區塊複製/貼上殼層。</span><span class="sxs-lookup"><span data-stu-id="8fd43-113">Click the **Try it** button on the code block below to launch the [Azure Cloud Shell](/azure/cloud-shell/) and copy/paste the script block into the shell.</span></span>

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

<span data-ttu-id="8fd43-114">請記下顯示的 **authKey** 和**端點**</span><span class="sxs-lookup"><span data-stu-id="8fd43-114">Make a note of the displayed **authKey** and **endpoint**</span></span> 

## <a name="downloading-and-running-the-application"></a><span data-ttu-id="8fd43-115">下載和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="8fd43-115">Downloading and running the application</span></span>

<span data-ttu-id="8fd43-116">讓我們來取得這個逐步解說的範例程式碼，並將其連線到您的 CosmosDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fd43-116">Let's get the sample code for this walkthrough and hook it up to your CosmosDB account.</span></span>

1. <span data-ttu-id="8fd43-117">下載範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="8fd43-117">Download the sample code.</span></span>  <span data-ttu-id="8fd43-118">您可以[從 GitHub 取得](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/)，或如果您有 [Git 命令列用戶端](https://git-scm.com/)，則使用下列命令將其複製到本機電腦：</span><span class="sxs-lookup"><span data-stu-id="8fd43-118">You can [get it from GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), or if you have the [git command line client](https://git-scm.com/), clone it to your local machine with the following command:</span></span>

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. <span data-ttu-id="8fd43-119">在 Visual Studio 中開啟 **todo.csproj**。</span><span class="sxs-lookup"><span data-stu-id="8fd43-119">Open **todo.csproj** in Visual Studio.</span></span>

3. <span data-ttu-id="8fd43-120">在 Web 專案中開啟 **appsettings.json**。</span><span class="sxs-lookup"><span data-stu-id="8fd43-120">Open **appsettings.json** in the web project.</span></span>  <span data-ttu-id="8fd43-121">尋找下列幾行︰</span><span class="sxs-lookup"><span data-stu-id="8fd43-121">Look for the following lines:</span></span>

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    <span data-ttu-id="8fd43-122">使用您先前記下的值取代 **AUTHKEYVALUE** 和 **ENDPOINTVALUE**。</span><span class="sxs-lookup"><span data-stu-id="8fd43-122">Replace **AUTHKEYVALUE** and **ENDPOINTVALUE** with the values you noted earlier.</span></span>

4. <span data-ttu-id="8fd43-123">按一下 **F5** 還原專案的 NuGet 套件，建置專案，並在本機執行。</span><span class="sxs-lookup"><span data-stu-id="8fd43-123">Press **F5** to restore the project's NuGet packages, build the project, and run it locally.</span></span>

<span data-ttu-id="8fd43-124">Web 應用程式應會在您的本機瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="8fd43-124">The web application should run locally in your browser.</span></span>  <span data-ttu-id="8fd43-125">按一下 [新建] 即可將新項目新增至待辦事項清單。</span><span class="sxs-lookup"><span data-stu-id="8fd43-125">You can add new items to the to-do list by clicking **Create New**.</span></span>  <span data-ttu-id="8fd43-126">請注意您在應用程式中輸入的資料會儲存至 CosmosDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fd43-126">Note the data you enter in the application is being stored in your CosmosDB account.</span></span>  <span data-ttu-id="8fd43-127">您可以[在 Azure 入口網站中檢視您的資料](/azure/documentdb/documentdb-view-json-document-explorer)。</span><span class="sxs-lookup"><span data-stu-id="8fd43-127">You can [view your data in the Azure portal](/azure/documentdb/documentdb-view-json-document-explorer).</span></span>

## <a name="deploying-the-application-as-an-azure-web-app"></a><span data-ttu-id="8fd43-128">將 Web 應用程式部署為 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8fd43-128">Deploying the application as an Azure Web App</span></span>

<span data-ttu-id="8fd43-129">您已成功建置使用 DocumentDB 等 Azure 服務的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8fd43-129">You've successfully built an application that uses Azure services like DocumentDB.</span></span>  <span data-ttu-id="8fd43-130">接下來，我們會將 Web 應用程式部署至雲端。</span><span class="sxs-lookup"><span data-stu-id="8fd43-130">Next, we'll deploy our web application to the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fd43-131">請務必使用與您的 Azure 訂用帳戶相關聯的相同帳戶登入 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8fd43-131">Be sure you're signed into Visual Studio with the same account your Azure subscription is associated with.</span></span>

1. <span data-ttu-id="8fd43-132">在 Visual Studio 方案總管中，以滑鼠右鍵按一下專案名稱，並選取 [發行...]</span><span class="sxs-lookup"><span data-stu-id="8fd43-132">In Visual Studio Solution Explorer, right-click on the project name and select **Publish...**</span></span>

2. <span data-ttu-id="8fd43-133">使用 [發佈] 對話方塊，選取 [Microsoft Azure App Service]，選取 [新建]，然後按一下 [發佈]</span><span class="sxs-lookup"><span data-stu-id="8fd43-133">Using the Publish dialog, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**</span></span>

3. <span data-ttu-id="8fd43-134">完成 [建立 App Service] 對話方塊，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8fd43-134">Complete the Create App Service dialog as follows:</span></span>

    * <span data-ttu-id="8fd43-135">輸入唯一 **Web 應用程式名稱**。</span><span class="sxs-lookup"><span data-stu-id="8fd43-135">Enter a unique **Web App Name**.</span></span>  <span data-ttu-id="8fd43-136">這會是應用程式 URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="8fd43-136">This will be part of the URL for your app.</span></span>
    * <span data-ttu-id="8fd43-137">選取您正在部署的 Azure **訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8fd43-137">Select the Azure **Subscription** you're deploying to.</span></span>  <span data-ttu-id="8fd43-138">使用與您稍早已登入 Cloud Shell 相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8fd43-138">Use same subscription with which you were logged into Cloud Shell earlier.</span></span>
    * <span data-ttu-id="8fd43-139">選取 Web 應用程式**資源群組**的 [DotNetAzureTutorial] 。</span><span class="sxs-lookup"><span data-stu-id="8fd43-139">Select *DotNetAzureTutorial* for the **Resource Group** for your web application.</span></span>
    * <span data-ttu-id="8fd43-140">選取或建立 **App Service 方案**來決定您應用程式的定價。</span><span class="sxs-lookup"><span data-stu-id="8fd43-140">Select or create an **App Service Plan** to determine the pricing your your application.</span></span>  <span data-ttu-id="8fd43-141">這裡有[更多關於 App Service 方案的資訊](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview)。</span><span class="sxs-lookup"><span data-stu-id="8fd43-141">Here's [more information about App Service Plans](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

4. <span data-ttu-id="8fd43-142">按一下 [建立] 以部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8fd43-142">Click **Create** to deploy the application.</span></span>  <span data-ttu-id="8fd43-143">部署完成時，瀏覽器會開啟已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8fd43-143">When deployment is complete, a browser will open with your deployed application.</span></span>

![已完成的應用程式](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="8fd43-145">清除</span><span class="sxs-lookup"><span data-stu-id="8fd43-145">Clean up</span></span>

<span data-ttu-id="8fd43-146">當您完成測試應用程式及檢查程式碼和資源時，可以透過刪除資源群組，將 Web 應用程式和 CosmosDB 帳戶刪除。</span><span class="sxs-lookup"><span data-stu-id="8fd43-146">When you're done testing the app and inspecting the code and resources, you can delete the Web App and CosmosDB account by deleting the resource group.</span></span> <span data-ttu-id="8fd43-147">在 Cloud Shell 中。</span><span class="sxs-lookup"><span data-stu-id="8fd43-147">in the Cloud Shell.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="8fd43-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8fd43-148">Next steps</span></span>

* [<span data-ttu-id="8fd43-149">在 ASP.NET Web 應用程式中使用驗證的 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fd43-149">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="8fd43-150">使用 Azure SQL Database 來建置 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8fd43-150">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="8fd43-151">使用 Azure 儲存體嘗試 .NET 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="8fd43-151">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


