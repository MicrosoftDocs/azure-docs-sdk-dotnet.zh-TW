---
title: 適用於 .NET 的 Azure IoT 程式庫
description: 適用於 .NET 的 Azure IoT 程式庫參考
ms.date: 10/19/2017
ms.topic: reference
ms.service: iot-hub
ms.openlocfilehash: 667663c5f5e3452fcc5ec0c4f3ded997370c5852
ms.sourcegitcommit: 7f1a1bf275d8489f8df266b746baa33d66fcb2c8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2018
ms.locfileid: "53737073"
---
# <a name="azure-iot-libraries-for-net"></a><span data-ttu-id="2cf18-103">適用於 .NET 的 Azure IoT 程式庫</span><span class="sxs-lookup"><span data-stu-id="2cf18-103">Azure IoT libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2cf18-104">概觀</span><span class="sxs-lookup"><span data-stu-id="2cf18-104">Overview</span></span>

<span data-ttu-id="2cf18-105">[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)是一項完全受控的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="2cf18-105">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="2cf18-106">IoT 解決方案中的裝置與資料來源，其範圍可以從簡單的網路連線感應器到功能強大的獨立計算裝置。</span><span class="sxs-lookup"><span data-stu-id="2cf18-106">Devices and data sources in an IoT solution can range from a simple network-connected sensor to a powerful, standalone computing device.</span></span> <span data-ttu-id="2cf18-107">裝置可能會有受限的處理能力、記憶體、通訊頻寬和通訊協定支援。</span><span class="sxs-lookup"><span data-stu-id="2cf18-107">Devices may have limited processing capability, memory, communication bandwidth, and communication protocol support.</span></span> <span data-ttu-id="2cf18-108">IoT [裝置 SDK](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) 可讓您實作各式各樣裝置和後端應用程式的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="2cf18-108">The IoT [device SDKs](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) enable you to implement client applications for a wide variety of devices and back-end applications.</span></span>

<span data-ttu-id="2cf18-109">適用於 .NET 的裝置 SDK 有助於建立執行 .NET 且連線到 Azure IoT 中樞的裝置。</span><span class="sxs-lookup"><span data-stu-id="2cf18-109">The device SDK for .NET facilitates building devices running .NET that connect to Azure IoT Hub.</span></span>

<span data-ttu-id="2cf18-110">適用於 .NET 的服務 SDK 有助於建立使用 .NET 且管理並允許雲端控制裝置的後端應用程式。</span><span class="sxs-lookup"><span data-stu-id="2cf18-110">The service SDK for .NET facilitates building back-end applications using .NET that manage and allow controlling devices from the Cloud.</span></span>

<span data-ttu-id="2cf18-111">[深入了解 Azure IoT](https://docs.microsoft.com/azure/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="2cf18-111">[Learn more about Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span></span>


## <a name="client-library"></a><span data-ttu-id="2cf18-112">用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="2cf18-112">Client library</span></span>

<span data-ttu-id="2cf18-113">使用 .NET IoT 裝置用戶端以連線並將訊息傳送至您的 IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="2cf18-113">Use the .NET IoT devices client to connect and send messages to your IoT Hub.</span></span>

<span data-ttu-id="2cf18-114">直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client)，或使用 [.NET Core CLI][DotNetCLI]。</span><span class="sxs-lookup"><span data-stu-id="2cf18-114">Install the [NuGet package]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2cf18-115">Visual Studio 套件管理員</span><span class="sxs-lookup"><span data-stu-id="2cf18-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a><span data-ttu-id="2cf18-116">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="2cf18-116">Code Examples</span></span> 

<span data-ttu-id="2cf18-117">這個範例會連線到 IoT 中樞，並每秒傳送一個訊息。</span><span class="sxs-lookup"><span data-stu-id="2cf18-117">This example connects to the IoT Hub and sends one message per second.</span></span>

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
var deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

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
> [<span data-ttu-id="2cf18-118">探索用戶端 API</span><span class="sxs-lookup"><span data-stu-id="2cf18-118">Explore the client APIs</span></span>](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a><span data-ttu-id="2cf18-119">範例</span><span class="sxs-lookup"><span data-stu-id="2cf18-119">Samples</span></span>

- [<span data-ttu-id="2cf18-120">事件中樞案例的一般 Web 服務</span><span class="sxs-lookup"><span data-stu-id="2cf18-120">Generic Web Service to Event Hub scenario</span></span>](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

<span data-ttu-id="2cf18-121">檢視 Azure IoT Upsamples 的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub)。</span><span class="sxs-lookup"><span data-stu-id="2cf18-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) of Azure IoT Upsamples.</span></span>

<span data-ttu-id="2cf18-122">如需詳細指引，請參閱 [Azure IoT 中樞開發人員指南](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide)。</span><span class="sxs-lookup"><span data-stu-id="2cf18-122">View the [Azure IoT Hub developer guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) for more guidance.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
