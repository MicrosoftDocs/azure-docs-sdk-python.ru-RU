---
title: "Сетевые библиотеки Azure для Python"
description: "Справочник по сетевым библиотекам Azure для Python"
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
ms.openlocfilehash: 47252ca3b2f5c6087277bac3735025f0dbabbdd8
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
---
# <a name="azure-network-libraries-for-python"></a><span data-ttu-id="b0d12-104">Сетевые библиотеки Azure для Python</span><span class="sxs-lookup"><span data-stu-id="b0d12-104">Azure Network libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="b0d12-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="b0d12-105">Overview</span></span>

<span data-ttu-id="b0d12-106">Ресурсы Azure можно подключать к [виртуальной сети Azure](/azure/virtual-network/virtual-networks-overview), а также к локальной сети.</span><span class="sxs-lookup"><span data-stu-id="b0d12-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) allows you to connect Azure resources, and also connect them to your on-premises network.</span></span>

<span data-ttu-id="b0d12-107">Чтобы приступить к работе с виртуальной сетью Azure, см. инструкции по [созданию виртуальной сети](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="b0d12-107">To get started with Azure Virtual Network, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-apis"></a><span data-ttu-id="b0d12-108">API управления</span><span class="sxs-lookup"><span data-stu-id="b0d12-108">Management APIs</span></span>

<span data-ttu-id="b0d12-109">Проверка, администрирование и настройка виртуальных сетей Azure с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="b0d12-109">Inspect, manage, and configure Azure virtual networks with the management APIs.</span></span>

<span data-ttu-id="b0d12-110">В отличие от других API-интерфейсов Azure для Python, сетевые API-интерфейсы явным образом разделены на пакеты по версиям.</span><span class="sxs-lookup"><span data-stu-id="b0d12-110">Unlike other Azure python APIs, the networking APIs are explicitly versioned into separage packages.</span></span> <span data-ttu-id="b0d12-111">Вам не нужно импортировать их по отдельности, так как сведения о пакете указаны в конструкторе клиента.</span><span class="sxs-lookup"><span data-stu-id="b0d12-111">You do not need to import them individually since the package information is specified in the client constructor.</span></span>

<span data-ttu-id="b0d12-112">Установите пакет управления с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="b0d12-112">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-network
```

### <a name="example"></a><span data-ttu-id="b0d12-113">Пример</span><span class="sxs-lookup"><span data-stu-id="b0d12-113">Example</span></span>

<span data-ttu-id="b0d12-114">Создайте виртуальную сеть и связанную с ней подсеть.</span><span class="sxs-lookup"><span data-stu-id="b0d12-114">Create a virtual network and an associated subnet.</span></span>

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
> [<span data-ttu-id="b0d12-115">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="b0d12-115">Explore the Management APIs</span></span>](/python/api/overview/azure/network/management)

### <a name="samples"></a><span data-ttu-id="b0d12-116">Примеры</span><span class="sxs-lookup"><span data-stu-id="b0d12-116">Samples</span></span>

* [<span data-ttu-id="b0d12-117">Начало работы с Azure Resource Manager для подсистем балансировки нагрузки на Python</span><span class="sxs-lookup"><span data-stu-id="b0d12-117">Getting started with Azure Resource Manager for load balancers in Python</span></span>](https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/)

<span data-ttu-id="b0d12-118">Просмотрите [полный список](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) примеров кода для виртуальных сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="b0d12-118">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) of Azure Virtual Network samples.</span></span>
