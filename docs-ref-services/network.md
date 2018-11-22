---
title: Сетевые библиотеки Azure для Python
description: Справочник по сетевым библиотекам Azure для Python
keywords: Azure, python, SDK, API, Network
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f468f844becc2f0fe07d892c725c00df4669f4e3
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52273030"
---
# <a name="azure-network-libraries-for-python"></a>Сетевые библиотеки Azure для Python

## <a name="overview"></a>Обзор

Ресурсы Azure можно подключать к [виртуальной сети Azure](/azure/virtual-network/virtual-networks-overview), а также к локальной сети.

Чтобы приступить к работе с виртуальной сетью Azure, см. инструкции по [созданию виртуальной сети](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-apis"></a>API управления

Проверка, администрирование и настройка виртуальных сетей Azure с помощью API управления.

В отличие от других API-интерфейсов Azure для Python, сетевые API-интерфейсы явным образом разделены на пакеты по версиям. Вам не нужно импортировать их по отдельности, так как сведения о пакете указаны в конструкторе клиента.

Установите пакет управления с помощью pip.

```bash
pip install azure-mgmt-network
```

### <a name="example"></a>Пример

Создайте виртуальную сеть и связанную с ней подсеть.

```python
from azure.mgmt.network import NetworkManagementClient

GROUP_NAME = 'resource-group'
VNET_NAME = 'your-vnet-identifier'
LOCATION = 'region'
SUBNET_NAME = 'your-subnet-identifier'

network_client = NetworkManagementClient(credentials, 'your-subscription-id')

async_vnet_creation = network_client.virtual_networks.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    {
        'location': LOCATION,
        'address_space': {
            'address_prefixes': ['10.0.0.0/16']
        }
    }
)
async_vnet_creation.wait()

# Create Subnet
async_subnet_creation = network_client.subnets.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    SUBNET_NAME,
    {'address_prefix': '10.0.0.0/24'}
)
subnet_info = async_subnet_creation.result()
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/network/management)

### <a name="samples"></a>Примеры

* [Начало работы с Azure Resource Manager для подсистем балансировки нагрузки на Python](https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/)

Просмотрите [полный список](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) примеров кода для виртуальных сетей Azure.
