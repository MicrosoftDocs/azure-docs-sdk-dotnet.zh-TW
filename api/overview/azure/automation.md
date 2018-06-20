---
title: 適用於 .NET 的 Azure 自動化文件庫
description: 適用於 .NET 的 Azure 自動化文件庫參考
keywords: Azure, .NET, SDK, API, 自動化
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: automation
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2055a5e24d445468763c049c34a5055cea108688
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2017
ms.locfileid: "23486691"
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="49b26-104">適用於 .NET 的 Azure 自動化文件庫</span><span class="sxs-lookup"><span data-stu-id="49b26-104">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="49b26-105">概觀</span><span class="sxs-lookup"><span data-stu-id="49b26-105">Overview</span></span>

<span data-ttu-id="49b26-106">Microsoft Azure 自動化可讓使用者將雲端和企業環境中經常執行的工作加以自動化。</span><span class="sxs-lookup"><span data-stu-id="49b26-106">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="49b26-107">如需詳細資訊，請參閱 [Azure 自動化概觀](/azure/automation/automation-intro)。</span><span class="sxs-lookup"><span data-stu-id="49b26-107">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="49b26-108">管理程式庫</span><span class="sxs-lookup"><span data-stu-id="49b26-108">Management library</span></span>

<span data-ttu-id="49b26-109">使用管理程式庫來管理 Runbook 和作業，並管理所需的狀態組態設定。</span><span class="sxs-lookup"><span data-stu-id="49b26-109">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="49b26-110">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="49b26-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="49b26-111">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="49b26-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="49b26-112">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="49b26-112">Code Example</span></span>

<span data-ttu-id="49b26-113">下列範例說明如何在現有的 Runbook 上啟動新的作業。</span><span class="sxs-lookup"><span data-stu-id="49b26-113">The following example illustrates how to start a new job based on an existing runbook.</span></span>

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
> [<span data-ttu-id="49b26-114">探索管理 API</span><span class="sxs-lookup"><span data-stu-id="49b26-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="49b26-115">範例</span><span class="sxs-lookup"><span data-stu-id="49b26-115">Samples</span></span>

* <span data-ttu-id="49b26-116">[AzureBot](https://github.com/Microsoft/AzureBot) 使用自動化程式庫搭配 [Bot Framework](https://docs.microsoft.com/bot-framework/) 和[認知服務](/cognitive-services)來提高 Azure 上的開發人員生產力</span><span class="sxs-lookup"><span data-stu-id="49b26-116">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="49b26-117">深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。</span><span class="sxs-lookup"><span data-stu-id="49b26-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
