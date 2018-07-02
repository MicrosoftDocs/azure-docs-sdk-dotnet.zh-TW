---
title: 適用於 .NET 的 Azure 自動化文件庫
description: 適用於 .NET 的 Azure 自動化文件庫參考
keywords: Azure, .NET, SDK, API, 自動化
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: automation
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e45db49fa71e5ad16ab1e4f26d76cd9b0146ac5f
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065758"
---
# <a name="azure-automation-libraries-for-net"></a>適用於 .NET 的 Azure 自動化文件庫

## <a name="overview"></a>概觀

Microsoft Azure 自動化可讓使用者將雲端和企業環境中經常執行的工作加以自動化。 

如需詳細資訊，請參閱 [Azure 自動化概觀](/azure/automation/automation-intro)。

## <a name="management-library"></a>管理程式庫

使用管理程式庫來管理 Runbook 和作業，並管理所需的狀態組態設定。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a>程式碼範例

下列範例說明如何在現有的 Runbook 上啟動新的作業。

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
> [探索管理 API](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a>範例

* [AzureBot](https://github.com/Microsoft/AzureBot) 使用自動化程式庫搭配 [Bot Framework](https://docs.microsoft.com/bot-framework/) 和[認知服務](/cognitive-services)來提高 Azure 上的開發人員生產力

深入探索可在應用程式中使用的 [.NET 程式碼範例](https://azure.microsoft.com/resources/samples/?platform=dotnet)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
