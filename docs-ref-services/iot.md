---
title: Библиотеки Центра Интернета вещей для Python
description: Справочник по библиотекам Центра Интернета вещей для Python
keywords: Azure, python, SDK, API, IoT Hub
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 0864c83eba43f97a606ae817f1a0ec2dd1ea787a
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52279247"
---
# <a name="azure-iot-hub-libraries-for-python"></a>Библиотеки Центра Интернета вещей для Python

## <a name="management-apipythonapioverviewazureiotmanagement"></a>[API управления](/python/api/overview/azure/iot/management)

```bash
pip install azure-mgmt-iothub
```

## <a name="create-the-management-client"></a>Создание клиента управления

Следующий код создает экземпляр клиента управления.

Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).

```python
from azure.mgmt.iothub import IotHubClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

iothub_client = IotHubClient(
    credentials,
    subscription_id
)
```

## <a name="create-an-iothub"></a>Создание Центра Интернета вещей
```python
async_iot_hub = iothub_client.iot_hub_resource.create_or_update(
    'MyResourceGroup',
    'MyIoTHubAccount',
    {
        'location': 'westus',
        'subscriptionid': subscription_id,
        'resourcegroup': 'MyResourceGroup',
        'sku': {
            'name': 'S1',
            'capacity': 2
        },
        'properties': {
            'enable_file_upload_notifications': False,
            'operations_monitoring_properties': {
            'events': {
                "C2DCommands": "Error",
                "DeviceTelemetry": "Error",
                "DeviceIdentityOperations": "Error",
                "Connections": "Information"
            }
            },
            "features": "None",
        }
    }
)
iothub = async_iot_hub.result() # Blocking wait for creation
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/iot/management)