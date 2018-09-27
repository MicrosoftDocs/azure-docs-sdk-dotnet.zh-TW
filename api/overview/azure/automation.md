---
title: 適用於 .NET 的 Azure 自動化文件庫
description: 適用於 .NET 的 Azure 自動化文件庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: automation
ms.openlocfilehash: 4890faab86d1319fe802a30e3735419ac65e8d64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190281"
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="65b1d-103">適用於 .NET 的 Azure 自動化文件庫</span><span class="sxs-lookup"><span data-stu-id="65b1d-103">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="65b1d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="65b1d-104">Overview</span></span>

<span data-ttu-id="65b1d-105">Microsoft Azure 自動化可讓使用者將雲端和企業環境中經常執行的工作加以自動化。</span><span class="sxs-lookup"><span data-stu-id="65b1d-105">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="65b1d-106">如需詳細資訊，請參閱 [Azure 自動化概觀](/azure/automation/automation-intro)。</span><span class="sxs-lookup"><span data-stu-id="65b1d-106">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="65b1d-107">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="65b1d-107">Management library</span></span>

<span data-ttu-id="65b1d-108">使用管理程式庫來管理 Runbook 和作業，並管理所需的狀態組態設定。</span><span class="sxs-lookup"><span data-stu-id="65b1d-108">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="65b1d-109">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="65b1d-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="65b1d-110">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="65b1d-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="65b1d-111">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="65b1d-111">Code Example</span></span>

<span data-ttu-id="65b1d-112">下列範例說明如何在現有的 Runbook 上啟動新的作業。</span><span class="sxs-lookup"><span data-stu-id="65b1d-112">The following example illustrates how to start a new job based on an existing runbook.</span></span>

```csharp
/*
  using Microsoft.Azure.Management.Automation;
*/
AutomationManagementClient client =
    new AutomationManagementClient(new CertificateCloudCredentials(subscriptionId, cert));

// Create job create parameters
JobCreateParameters jcParam = new JobCreateParameters
{
    Properties = new JobCreateProperties
    {
        Runbook = new RunbookAssociationProperty
        {
            Name = runbookName
        },
        Parameters = null // optional parameters here
    }
};

// create runbook job. This gives back the Job
Job job = automationManagementClient.Jobs.Create(automationAccountName, jcParam).Job;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="65b1d-113">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="65b1d-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="65b1d-114">範例</span><span class="sxs-lookup"><span data-stu-id="65b1d-114">Samples</span></span>

* <span data-ttu-id="65b1d-115">[AzureBot](https://github.com/Microsoft/AzureBot) 使用自動化程式庫搭配 [Bot Framework](https://docs.microsoft.com/bot-framework/) 和[認知服務](/cognitive-services)來提高 Azure 上的開發人員生產力</span><span class="sxs-lookup"><span data-stu-id="65b1d-115">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="65b1d-116">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="65b1d-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
