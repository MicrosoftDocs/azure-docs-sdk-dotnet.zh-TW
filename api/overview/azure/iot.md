---
title: 適用於 .NET 的 Azure IoT 程式庫
description: 適用於 .NET 的 Azure IoT 程式庫參考
keywords: Azure, .NET, SDK, API, IoT
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: iot-hub
ms.custom: devcenter, svc-overview
ms.openlocfilehash: af823e910acedd4f204034b12a31ba61fd53e090
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065268"
---
# <a name="azure-iot-libraries-for-net"></a><span data-ttu-id="37b06-104">適用於 .NET 的 Azure IoT 程式庫</span><span class="sxs-lookup"><span data-stu-id="37b06-104">Azure IoT libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="37b06-105">概觀</span><span class="sxs-lookup"><span data-stu-id="37b06-105">Overview</span></span>

<span data-ttu-id="37b06-106">[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)是一項完全受控的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="37b06-106">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="37b06-107">IoT 解決方案中的裝置與資料來源，其範圍可以從簡單的網路連線感應器到功能強大的獨立計算裝置。</span><span class="sxs-lookup"><span data-stu-id="37b06-107">Devices and data sources in an IoT solution can range from a simple network-connected sensor to a powerful, standalone computing device.</span></span> <span data-ttu-id="37b06-108">裝置可能會有受限的處理能力、記憶體、通訊頻寬和通訊協定支援。</span><span class="sxs-lookup"><span data-stu-id="37b06-108">Devices may have limited processing capability, memory, communication bandwidth, and communication protocol support.</span></span> <span data-ttu-id="37b06-109">IoT [裝置 SDK](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) 可讓您實作各式各樣裝置和後端應用程式的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="37b06-109">The IoT [device SDKs](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) enable you to implement client applications for a wide variety of devices and back-end applications.</span></span>

<span data-ttu-id="37b06-110">適用於 .NET 的裝置 SDK 有助於建立執行 .NET 且連線到 Azure IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="37b06-110">The device SDK for .NET facilitates building devices running .NET that connect to Azure IoT Hub.</span></span>

<span data-ttu-id="37b06-111">適用於 .NET 的服務 SDK 有助於建立使用 .NET 且管理並允許雲端控制裝置的後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="37b06-111">The service SDK for .NET facilitates building back-end applications using .NET that manage and allow controlling devices from the Cloud.</span></span>

<span data-ttu-id="37b06-112">[深入了解 Azure IoT](https://docs.microsoft.com/azure/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="37b06-112">[Learn more about Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span></span>


## <a name="client-library"></a><span data-ttu-id="37b06-113">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="37b06-113">Client library</span></span>

<span data-ttu-id="37b06-114">使用 .NET IoT 裝置用戶端以連線並將訊息傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="37b06-114">Use the .NET IoT devices client to connect and send messages to your IoT Hub.</span></span>

<span data-ttu-id="37b06-115">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="37b06-115">Install the [NuGet package]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="37b06-116">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="37b06-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a><span data-ttu-id="37b06-117">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="37b06-117">Code Examples</span></span> 

<span data-ttu-id="37b06-118">這個範例會連線到 IoT 中樞，並每秒傳送一個訊息。</span><span class="sxs-lookup"><span data-stu-id="37b06-118">This example connects to the IoT Hub and sends one message per second.</span></span>

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
DeviceAuthenticationWithRegistrySymmetricKeyvar deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

DeviceClient deviceClient = DeviceClient.Create(iotHubHostName, deviceAuthentication, TransportType.Mqtt);

while (true)
{
    double currentTemperature = 20 + Rand.NextDouble() * 15;
    double currentHumidity = 60 + Rand.NextDouble() * 20;

    var telemetryDataPoint = new
    {
        messageId = _messageId++,
        deviceId = deviceId,
        temperature = currentTemperature,
        humidity = currentHumidity
    };
    string messageString = JsonConvert.SerializeObject(telemetryDataPoint);
    Message message = new Message(Encoding.ASCII.GetBytes(messageString));
    message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

    await deviceClient.SendEventAsync(message);
    Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

    await Task.Delay(1000);
}
```


> [!div class="nextstepaction"]
> [<span data-ttu-id="37b06-119">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="37b06-119">Explore the client APIs</span></span>](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a><span data-ttu-id="37b06-120">範例</span><span class="sxs-lookup"><span data-stu-id="37b06-120">Samples</span></span>

- [<span data-ttu-id="37b06-121">事件中樞案例的一般 Web 服務</span><span class="sxs-lookup"><span data-stu-id="37b06-121">Generic Web Service to Event Hub scenario</span></span>](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

<span data-ttu-id="37b06-122">檢視 Azure IoT Upsamples 的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub)。</span><span class="sxs-lookup"><span data-stu-id="37b06-122">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) of Azure IoT Upsamples.</span></span>

<span data-ttu-id="37b06-123">如需詳細指引，請參閱 [Azure IoT 中樞開發人員指南](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide)。</span><span class="sxs-lookup"><span data-stu-id="37b06-123">View the [Azure IoT Hub developer guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) for more guidance.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
