---
title: Библиотеки авторизации Azure для Python
description: Справочник по библиотекам авторизации Azure для Python
keywords: Azure, python, SDK, API, Authorization
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: c7c4af34e82f2baad39635ecd20f1b9c48900b41
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534366"
---
# <a name="azure-authorization-libraries-for-python"></a><span data-ttu-id="64bc3-104">Библиотеки авторизации Azure для Python</span><span class="sxs-lookup"><span data-stu-id="64bc3-104">Azure Authorization libraries for python</span></span>

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[<span data-ttu-id="64bc3-105">API управления</span><span class="sxs-lookup"><span data-stu-id="64bc3-105">Management API</span></span>](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a><span data-ttu-id="64bc3-106">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="64bc3-106">Create the management client</span></span>

<span data-ttu-id="64bc3-107">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="64bc3-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="64bc3-108">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="64bc3-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="64bc3-109">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="64bc3-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password'       # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
```

## <a name="check-permissions-for-a-resource-group"></a><span data-ttu-id="64bc3-110">Проверка разрешений для группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="64bc3-110">Check permissions for a resource group</span></span>

<span data-ttu-id="64bc3-111">Следующий код проверяет разрешения в указанной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="64bc3-111">The following code checks permissions in a given resource group.</span></span> <span data-ttu-id="64bc3-112">См. дополнительные сведения о [создании групп ресурсов и управлении ими](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="64bc3-112">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="64bc3-113">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="64bc3-113">Explore the Management APIs</span></span>](/python/api/overview/azure/authorization/management)
