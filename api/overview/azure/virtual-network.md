---
title: "適用於 .NET 的 Azure 虛擬網路程式庫"
description: "適用於 .NET 的 Azure 虛擬網路程式庫參考"
keywords: "Azure, .NET, SDK, API, 虛擬網路"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/01/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: ea605dbd632ef4deb9c97c8de3474246dd4be30d
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-network-libraries-for-net"></a><span data-ttu-id="37d31-104">適用於 .NET 的 Azure 虛擬網路程式庫</span><span class="sxs-lookup"><span data-stu-id="37d31-104">Azure Virtual Network libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="37d31-105">概觀</span><span class="sxs-lookup"><span data-stu-id="37d31-105">Overview</span></span>
<span data-ttu-id="37d31-106">[Azure 虛擬網路服務](/azure/virtual-network/virtual-networks-overview)可讓 Azure 資源與虛擬網路 (VNet) 安全地彼此連線。</span><span class="sxs-lookup"><span data-stu-id="37d31-106">The [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) service enables you to securely connect Azure resources to each other with virtual networks (VNets).</span></span> <span data-ttu-id="37d31-107">VNet 是您的網路在雲端中的身分。</span><span class="sxs-lookup"><span data-stu-id="37d31-107">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="37d31-108">您也可以將 VNet 互相連線，讓連線至任一 VNet 的資源能夠彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="37d31-108">You can also connect VNets to each other, enabling resources connected to either VNet to communicate with each other.</span></span> 

## <a name="management-library"></a><span data-ttu-id="37d31-109">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="37d31-109">Management library</span></span>

<span data-ttu-id="37d31-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="37d31-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="37d31-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="37d31-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="37d31-112">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="37d31-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a><span data-ttu-id="37d31-113">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="37d31-113">Code Example</span></span>
<span data-ttu-id="37d31-114">此範例會示範如何建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="37d31-114">This example shows how you can create a virtual network.</span></span>

```csharp
/* 
  Include these "using" directives...
  
  using Microsoft.Azure.Management.Network.Fluent;
  using Microsoft.Azure.Management.Network.Fluent.Models;
*/
using (NetworkManagementClient client = new NetworkManagementClient(credentials))
{
    // Define VNet
    VirtualNetworkInner vnet = new VirtualNetworkInner()
    {
        Location = "West US",
        AddressSpace = new AddressSpace()
        {
            AddressPrefixes = new List<string>() { "0.0.0.0/16" }
        },

        DhcpOptions = new DhcpOptions()
        {
            DnsServers = new List<string>() { "1.1.1.1", "1.1.2.4" }
        },

        Subnets = new List<Subnet>()
        {
            new Subnet()
            {
                Name = subnet1Name,
                AddressPrefix = "1.0.1.0/24",
            },
            new Subnet()
            {
                Name = subnet2Name,
               AddressPrefix = "1.0.2.0/24",
            }
        }
    };
    
    await client.VirtualNetworks.CreateOrUpdateAsync(resourceGroupName, vNetName, vnet);
}

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="37d31-115">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="37d31-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a><span data-ttu-id="37d31-116">範例</span><span class="sxs-lookup"><span data-stu-id="37d31-116">Samples</span></span>
- [<span data-ttu-id="37d31-117">使用子網路管理虛擬網路</span><span class="sxs-lookup"><span data-stu-id="37d31-117">Managing Virtual Networks with subnets</span></span>](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

<span data-ttu-id="37d31-118">深入探索可在應用程式中使用的 [.NET 範例程式碼](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="37d31-118">Explore more [.NET sample code](https://azure.microsoft.com/resources/samples/?platform=dotnet) that you can use in your apps.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

