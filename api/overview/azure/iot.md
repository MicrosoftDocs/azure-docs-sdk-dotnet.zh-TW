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
# <a name="azure-iot-libraries-for-net"></a>適用於 .NET 的 Azure IoT 程式庫

## <a name="overview"></a>概觀

[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)是一項完全受控的服務，可在數百萬個裝置和一個解決方案後端之間啟用可靠且安全的雙向通訊。

IoT 解決方案中的裝置與資料來源，其範圍可以從簡單的網路連線感應器到功能強大的獨立計算裝置。 裝置可能會有受限的處理能力、記憶體、通訊頻寬和通訊協定支援。 IoT [裝置 SDK](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) 可讓您實作各式各樣裝置和後端應用程式的用戶端應用程式。

適用於 .NET 的裝置 SDK 有助於建立執行 .NET 且連線到 Azure IoT 中樞的裝置。

適用於 .NET 的服務 SDK 有助於建立使用 .NET 且管理並允許雲端控制裝置的後端應用程式。

[深入了解 Azure IoT](https://docs.microsoft.com/azure/iot-hub/)。


## <a name="client-library"></a>用戶端程式庫

使用 .NET IoT 裝置用戶端以連線並將訊息傳送至您的 IoT 中樞。

直接從 Visual Studio [套件管理員主控台][PackageManager]安裝 [NuGet 套件]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client)，或使用 [.NET Core CLI][DotNetCLI]。

#### <a name="visual-studio-package-manager"></a>Visual Studio 套件管理員

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a>程式碼範例 

這個範例會連線到 IoT 中樞，並每秒傳送一個訊息。

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
> [探索用戶端 API](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a>範例

- [事件中樞案例的一般 Web 服務](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

檢視 Azure IoT Upsamples 的[完整清單](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub)。

如需詳細指引，請參閱 [Azure IoT 中樞開發人員指南](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide)。

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
