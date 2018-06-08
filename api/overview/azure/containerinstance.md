---
title: 適用於 .NET 的 Azure 容器執行個體程式庫
description: 適用於 .NET 的 Azure 容器執行個體程式庫參考
keywords: Azure, .NET, SDK, API, 容器執行個體, ACI
author: mmacy
ms.author: marsma
manager: jeconnoc
ms.date: 05/25/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: dcontainer-instances
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 033f67a989b0ed6cfcb67a6212c0d5c46c485afa
ms.sourcegitcommit: 4ae9f77a9300a4fe54d0179055ae61191078f207
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2018
ms.locfileid: "34567178"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="ab9e3-104">適用於 .NET 的 Azure 容器執行個體程式庫</span><span class="sxs-lookup"><span data-stu-id="ab9e3-104">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="ab9e3-105">使用適用於 .NET 的 Microsoft Azure 容器執行個體程式庫，來建立和管理 Azure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-105">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="ab9e3-106">如需詳細資訊，請參閱 [Azure 容器執行個體概觀](/azure/container-instances/container-instances-overview)。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="ab9e3-107">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="ab9e3-107">Management library</span></span>

<span data-ttu-id="ab9e3-108">使用管理程式庫來建立和管理 Azure 中的 Azure 容器執行個體。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="ab9e3-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="ab9e3-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="ab9e3-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="examples"></a><span data-ttu-id="ab9e3-111">範例</span><span class="sxs-lookup"><span data-stu-id="ab9e3-111">Examples</span></span>

### <a name="create-container-group---single-container"></a><span data-ttu-id="ab9e3-112">建立容器群組 - 單一容器</span><span class="sxs-lookup"><span data-stu-id="ab9e3-112">Create container group - single container</span></span>

<span data-ttu-id="ab9e3-113">此範例會建立一個容器群組搭配單一容器。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-113">This example creates a container group with a single container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a><span data-ttu-id="ab9e3-114">建立容器群組 - 多個容器</span><span class="sxs-lookup"><span data-stu-id="ab9e3-114">Create container group - multiple containers</span></span>

<span data-ttu-id="ab9e3-115">此範例會建立一個容器群組搭配兩個容器：分別是應用程式容器和側車容器。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-115">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="ab9e3-116">使用輪詢建立非同步容器</span><span class="sxs-lookup"><span data-stu-id="ab9e3-116">Asynchronous container create with polling</span></span>

<span data-ttu-id="ab9e3-117">此範例會使用非同步建立方式，來建立一個容器群組搭配單一容器。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-117">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="ab9e3-118">接著，會輪詢 Azure 容器群組，再輸出容器群組的狀態，直到狀態顯示為「執行中」為止。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-118">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a><span data-ttu-id="ab9e3-119">立工作型容器群組</span><span class="sxs-lookup"><span data-stu-id="ab9e3-119">Create task-based container group</span></span>

<span data-ttu-id="ab9e3-120">此範例會建立一個容器群組搭配單一工作型容器。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-120">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="ab9e3-121">該容器會以「絕不」[重新啟動原則](/azure/container-instances/container-instances-restart-policy)和[自訂命令列](/azure/container-instances/container-instances-restart-policy#command-line-override)來設定。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-121">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="ab9e3-122">如果您想要使用數個命令列引數執行單一命令，例如 `echo FOO BAR`，則必須以字串陣列方式提供給 `WithStartingCommandLines` 方法。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-122">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="ab9e3-123">例如︰</span><span class="sxs-lookup"><span data-stu-id="ab9e3-123">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="ab9e3-124">然而，如果您想要(或可能會) 使用多個引數來執行多個命令，則必須執行殼層，並將鏈結的命令做為引數傳遞。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-124">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="ab9e3-125">例如，這樣會執行 `echo` 和 `tail` 命令：</span><span class="sxs-lookup"><span data-stu-id="ab9e3-125">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a><span data-ttu-id="ab9e3-126">列出容器群組</span><span class="sxs-lookup"><span data-stu-id="ab9e3-126">List container groups</span></span>

<span data-ttu-id="ab9e3-127">此範例會列出資源群組中的容器群組。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-127">This example lists the container groups in a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a><span data-ttu-id="ab9e3-128">取得現有的容器群組</span><span class="sxs-lookup"><span data-stu-id="ab9e3-128">Get an existing container group</span></span>

<span data-ttu-id="ab9e3-129">此範例會取得位於資源群組中的特定容器群組，且會列印出這些容器群組的屬性和值。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-129">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a><span data-ttu-id="ab9e3-130">刪除容器群組</span><span class="sxs-lookup"><span data-stu-id="ab9e3-130">Delete a container group</span></span>

<span data-ttu-id="ab9e3-131">此範例會從資源群組中刪除容器群組。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-131">This example deletes a container group from a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a><span data-ttu-id="ab9e3-132">API 參考資料</span><span class="sxs-lookup"><span data-stu-id="ab9e3-132">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab9e3-133">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="ab9e3-133">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="ab9e3-134">範例</span><span class="sxs-lookup"><span data-stu-id="ab9e3-134">Samples</span></span>

* <span data-ttu-id="ab9e3-135">您可以在 GitHub 中找到先前範例的原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="ab9e3-135">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="ab9e3-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="ab9e3-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="ab9e3-137">更多 Azure 容器執行個體程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="ab9e3-137">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="ab9e3-138">[Azure 程式碼範例][samples]</span><span class="sxs-lookup"><span data-stu-id="ab9e3-138">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="ab9e3-139">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="ab9e3-139">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
