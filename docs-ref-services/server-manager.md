---
title: Библиотеки диспетчера серверов Azure для Python
description: Справочник по библиотекам диспетчера серверов Azure для Python
keywords: Azure, python, SDK, API, Server Manager
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 480513a76683c97fdac8d2a65b38fde0fffb6dcd
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479237"
---
# <a name="azure-server-manager-libraries-for-python"></a><span data-ttu-id="f44bc-104">Библиотеки диспетчера серверов Azure для Python</span><span class="sxs-lookup"><span data-stu-id="f44bc-104">Azure Server Manager libraries for python</span></span>

## <a name="management-apipythonapioverviewazureservermanagermanagement"></a>[<span data-ttu-id="f44bc-105">API управления</span><span class="sxs-lookup"><span data-stu-id="f44bc-105">Management API</span></span>](/python/api/overview/azure/servermanager/management)

```bash
pip install azure-mgmt-servermanager
```

## <a name="create-the-management-client"></a><span data-ttu-id="f44bc-106">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="f44bc-106">Create the management client</span></span>

<span data-ttu-id="f44bc-107">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="f44bc-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="f44bc-108">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="f44bc-108">You will need to provide your ``subscription_id`` which can be retrieved from your [subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="f44bc-109">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="f44bc-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.servermanager import ServerManagement
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

servermanager_client = ServerManagement(
    credentials,
    subscription_id
)
``` 

## <a name="create-gateway"></a><span data-ttu-id="f44bc-110">Создание шлюза</span><span class="sxs-lookup"><span data-stu-id="f44bc-110">Create gateway</span></span>
```python
gateway_async = servermanager_client.gateway.create(
    'MyResourceGroup',
    'MyGateway',
    'centralus'
)
gateway = gateway_async.result() # Blocking wait
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f44bc-111">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="f44bc-111">Explore the Management APIs</span></span>](/python/api/overview/azure/servermanager/management)