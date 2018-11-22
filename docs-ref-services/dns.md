---
title: Библиотеки Azure DNS для Python
description: Справочник по библиотекам Azure DNS для Python
keywords: Azure, python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: c70c3d44911b28b0a8c92b5f7efeca3bf1611f43
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277256"
---
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="7aed1-104">Библиотеки Azure DNS для Python</span><span class="sxs-lookup"><span data-stu-id="7aed1-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="7aed1-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="7aed1-105">Overview</span></span>

<span data-ttu-id="7aed1-106">[Azure DNS](/azure/dns/dns-overview) — это служба размещения для доменов DNS, которая предоставляет разрешение имен DNS с помощью инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="7aed1-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="7aed1-107">Чтобы приступить к работе с Azure DNS, см. инструкции по [началу работы с Azure DNS с помощью портала Azure](/azure/dns/dns-getstarted-portal).</span><span class="sxs-lookup"><span data-stu-id="7aed1-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apipythonapioverviewazurednsmanagement"></a>[<span data-ttu-id="7aed1-108">API управления</span><span class="sxs-lookup"><span data-stu-id="7aed1-108">Management API</span></span>](/python/api/overview/azure/dns/management)

```bash
pip install azure-mgmt-dns
```

## <a name="create-the-management-client"></a><span data-ttu-id="7aed1-109">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="7aed1-109">Create the management client</span></span>

<span data-ttu-id="7aed1-110">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="7aed1-110">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="7aed1-111">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="7aed1-111">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="7aed1-112">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="7aed1-112">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python 
from azure.mgmt.dns import DnsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

dns_client = DnsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="create-dns-zone"></a><span data-ttu-id="7aed1-113">Создание зоны DNS</span><span class="sxs-lookup"><span data-stu-id="7aed1-113">Create DNS zone</span></span>
```python
# The only valid value is 'global', otherwise you will get a:
# The subscription is not registered for the resource type 'dnszones' in the location 'westus'.
zone = dns_client.zones.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    {
            'zone_type': 'Public', # or Private
        'location': 'global'
    }
)
```
    
## <a name="create-a-record-set"></a><span data-ttu-id="7aed1-114">Создание набора записей</span><span class="sxs-lookup"><span data-stu-id="7aed1-114">Create a Record Set</span></span>
```python
record_set = dns_client.record_sets.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    'MyRecordSet',
    'A',
    {
            "ttl": 300,
            "arecords": [
                {
                "ipv4_address": "1.2.3.4"
                },
                {
                "ipv4_address": "1.2.3.5"
                }
            ]
    }
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7aed1-115">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="7aed1-115">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/management)
