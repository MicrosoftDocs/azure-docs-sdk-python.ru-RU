---
title: Библиотеки Azure Commerce для Python
description: Справочник по библиотекам Azure Commerce для Python
keywords: Azure, python, SDK, API, Commerce
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 4d7685601fe671f7d6708b763789b42429c2f18e
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534339"
---
# <a name="azure-commerce-libraries-for-python"></a><span data-ttu-id="c2227-104">Библиотеки Azure Commerce для Python</span><span class="sxs-lookup"><span data-stu-id="c2227-104">Azure Commerce libraries for python</span></span>

## <a name="management-apipythonapioverviewazurecommercemanagement"></a>[<span data-ttu-id="c2227-105">API управления</span><span class="sxs-lookup"><span data-stu-id="c2227-105">Management API</span></span>](/python/api/overview/azure/commerce/management)

```bash
pip install azure-mgmt-commerce
```
## <a name="create-the-commerce-client"></a><span data-ttu-id="c2227-106">Создание коммерческого клиента</span><span class="sxs-lookup"><span data-stu-id="c2227-106">Create the commerce client</span></span>

<span data-ttu-id="c2227-107">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="c2227-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="c2227-108">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="c2227-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="c2227-109">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="c2227-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.commerce import UsageManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

commerce_client = UsageManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="get-rate-card"></a><span data-ttu-id="c2227-110">Получение тарифной карты</span><span class="sxs-lookup"><span data-stu-id="c2227-110">Get rate card</span></span>

```python
# OfferDurableID: https://azure.microsoft.com/en-us/support/legal/offer-details/
rate = commerce_client.rate_card.get(
    "OfferDurableId eq 'MS-AZR-0062P' and Currency eq 'USD' and Locale eq 'en-US' and RegionInfo eq 'US'"
)
```

## <a name="get-usage"></a><span data-ttu-id="c2227-111">Получение сведений об использовании</span><span class="sxs-lookup"><span data-stu-id="c2227-111">Get Usage</span></span>

```python
from datetime import date, timedelta

# Takes onky dates in full ISO8601 with 'T00:00:00Z'
# Return an iterator like object: https://docs.python.org/3/library/stdtypes.html#iterator-types
usage_iterator = commerce_client.usage_aggregates.list(
    str(date.today() - timedelta(days=1))+'T00:00:00Z',
    str(date.today())+'T00:00:00Z'
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2227-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="c2227-112">Explore the Management APIs</span></span>](/python/api/overview/azure/commerce/management)