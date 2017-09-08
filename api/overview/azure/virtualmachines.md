---
title: "適用於 .NET 的 Azure 計算"
description: "適用於 .NET 的 Azure 計算程式庫參考"
keywords: "Azure, .NET, SDK, API, VM, 虛擬機器, 計算"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: b30c1433b8f25941fc1d4ea4718aa07c0a870580
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-machine-libraries-for-net"></a><span data-ttu-id="eb509-104">適用於 .NET 的 Azure 虛擬機器程式庫</span><span class="sxs-lookup"><span data-stu-id="eb509-104">Azure virtual machine libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="eb509-105">概觀</span><span class="sxs-lookup"><span data-stu-id="eb509-105">Overview</span></span>

<span data-ttu-id="eb509-106">執行 Linux 或 Windows 並可視需要擴充的計算資源。</span><span class="sxs-lookup"><span data-stu-id="eb509-106">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="eb509-107">若要開始使用 Azure 虛擬機器，請參閱[使用 Azure 入口網站建立 Linux 虛擬機器](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)。</span><span class="sxs-lookup"><span data-stu-id="eb509-107">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="eb509-108">管理 API</span><span class="sxs-lookup"><span data-stu-id="eb509-108">Management APIs</span></span>

<span data-ttu-id="eb509-109">從程式碼使用管理 API 在 Azure 中建立、設定及相應放大 Windows 和 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="eb509-109">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="eb509-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="eb509-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="eb509-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="eb509-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="eb509-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="eb509-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a><span data-ttu-id="eb509-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="eb509-113">Code Example</span></span>

<span data-ttu-id="eb509-114">建立 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="eb509-114">Create a Windows VM.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IVirtualMachine windowsVM = azure.VirtualMachines.Define("MyVirtualMachine")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress("MyIPAddressLabel")
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername("UserName")
    .WithAdminPassword("Password")
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb509-115">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="eb509-115">Explore the management APIs</span></span>](https://review.docs.microsoft.com/en-us/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a><span data-ttu-id="eb509-116">範例</span><span class="sxs-lookup"><span data-stu-id="eb509-116">Samples</span></span>

* [<span data-ttu-id="eb509-117">建立和管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="eb509-117">Create and manage virtual machines</span></span>](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [<span data-ttu-id="eb509-118">使用 .NET 以範本部署已啟用 SSH 的 VM</span><span class="sxs-lookup"><span data-stu-id="eb509-118">Deploy an SSH-enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/)

<span data-ttu-id="eb509-119">檢視虛擬機器範本的[完整清單](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM)。</span><span class="sxs-lookup"><span data-stu-id="eb509-119">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) of virtual machine samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
