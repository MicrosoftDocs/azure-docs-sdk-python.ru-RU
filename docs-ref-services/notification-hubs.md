---
title: Библиотеки Центров уведомлений Azure для Python
description: Справочник по библиотекам Центров уведомлений Azure для Python
keywords: Azure, python, SDK, API, Notification Hubs
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f600b28c347cdbffc16342da25a72e4de8e83c5f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534246"
---
# <a name="azure-notification-hubs-libraries-for-python"></a><span data-ttu-id="ff265-104">Библиотеки Центров уведомлений Azure для Python</span><span class="sxs-lookup"><span data-stu-id="ff265-104">Azure Notification Hubs libraries for python</span></span>

## <a name="management-apipythonapioverviewazurenotificationhubsmanagement"></a>[<span data-ttu-id="ff265-105">API управления</span><span class="sxs-lookup"><span data-stu-id="ff265-105">Management API</span></span>](/python/api/overview/azure/notificationhubs/management)

```bash
pip install azure-mgmt-notificationhubs
```

## <a name="create-the-management-client"></a><span data-ttu-id="ff265-106">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="ff265-106">Create the management client</span></span>

<span data-ttu-id="ff265-107">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="ff265-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="ff265-108">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="ff265-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="ff265-109">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="ff265-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

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

## <a name="check-namespace-availability"></a><span data-ttu-id="ff265-110">Проверка доступности пространства имен</span><span class="sxs-lookup"><span data-stu-id="ff265-110">Check namespace availability</span></span>

<span data-ttu-id="ff265-111">Следующий код проверяет доступность пространства имен концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ff265-111">The following code check namespace availability of a notification hub.</span></span>

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
> [<span data-ttu-id="ff265-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="ff265-112">Explore the Management APIs</span></span>](/python/api/overview/azure/notificationhubs/management)
