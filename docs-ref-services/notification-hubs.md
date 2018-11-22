---
title: Библиотеки Центров уведомлений Azure для Python
description: Справочник по библиотекам Центров уведомлений Azure для Python
keywords: Azure, python, SDK, API, Notification Hubs
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 3a9cc087d315ee2a274d3ef00623b304280017e5
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277246"
---
# <a name="azure-notification-hubs-libraries-for-python"></a><span data-ttu-id="e7754-104">Библиотеки Центров уведомлений Azure для Python</span><span class="sxs-lookup"><span data-stu-id="e7754-104">Azure Notification Hubs libraries for python</span></span>

## <a name="management-apipythonapioverviewazurenotificationhubsmanagement"></a>[<span data-ttu-id="e7754-105">API управления</span><span class="sxs-lookup"><span data-stu-id="e7754-105">Management API</span></span>](/python/api/overview/azure/notificationhubs/management)

```bash
pip install azure-mgmt-notificationhubs
```

## <a name="create-the-management-client"></a><span data-ttu-id="e7754-106">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="e7754-106">Create the management client</span></span>

<span data-ttu-id="e7754-107">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="e7754-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="e7754-108">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="e7754-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="e7754-109">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="e7754-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.notificationhubs import NotificationHubsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

redis_client = NotificationHubsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="check-namespace-availability"></a><span data-ttu-id="e7754-110">Проверка доступности пространства имен</span><span class="sxs-lookup"><span data-stu-id="e7754-110">Check namespace availability</span></span>

<span data-ttu-id="e7754-111">Следующий код проверяет доступность пространства имен концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="e7754-111">The following code check namespace availability of a notification hub.</span></span>
```python
from azure.mgmt.notificationhubs.models import CheckAvailabilityParameters

account_name = 'mynotificationhub'
output = notificationhubs_client.namespaces.check_availability(
    azure.mgmt.notificationhubs.models.CheckAvailabilityParameters(
        name = account_name
    )
)
# output is a CheckAvailibilityResource instance
print(output.is_availiable) # Yes, it's 'availiable', it's a typo in the REST API
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7754-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="e7754-112">Explore the Management APIs</span></span>](/python/api/overview/azure/notificationhubs/management)
