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
# <a name="azure-virtual-machine-libraries-for-net"></a>適用於 .NET 的 Azure 虛擬機器程式庫

## <a name="overview"></a>概觀

執行 Linux 或 Windows 並可視需要擴充的計算資源。

若要開始使用 Azure 虛擬機器，請參閱[使用 Azure 入口網站建立 Linux 虛擬機器](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)。

## <a name="management-apis"></a>管理 API

從程式碼使用管理 API 在 Azure 中建立、設定及相應放大 Windows 和 Linux 虛擬機器。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a>.NET Core CLI

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a>程式碼範例

建立 Windows VM。

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
> [探索管理 API](https://review.docs.microsoft.com/en-us/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a>範例

* [建立和管理虛擬機器](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [使用 .NET 以範本部署已啟用 SSH 的 VM](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/)

檢視虛擬機器範本的[完整清單](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
