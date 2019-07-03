---
title: Библиотеки Azure DevTest Labs для Python
description: Справочник по библиотекам Azure DevTest Labs для Python
keywords: Azure, python, SDK, API, DevTest Labs
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f232a24dfba610b3fdf505b63788aecc7b8fa9f9
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534286"
---
# <a name="azure-devtest-labs-libraries-for-python"></a><span data-ttu-id="caab3-104">Библиотеки Azure DevTest Labs для Python</span><span class="sxs-lookup"><span data-stu-id="caab3-104">Azure DevTest Labs libraries for python</span></span>

## <a name="management-apipythonapioverviewazuredevtestlabsmanagement"></a>[<span data-ttu-id="caab3-105">API управления</span><span class="sxs-lookup"><span data-stu-id="caab3-105">Management API</span></span>](/python/api/overview/azure/devtestlabs/management)

```bash
pip install azure-mgmt-devtestlabs
```

## <a name="create-the-management-client"></a><span data-ttu-id="caab3-106">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="caab3-106">Create the management client</span></span>

<span data-ttu-id="caab3-107">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="caab3-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="caab3-108">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="caab3-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="caab3-109">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="caab3-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.devtestlabs import DevTestLabsClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

devtestlabs_client = DevTestLabsClient(
    credentials,
    subscription_id
)
```

## <a name="create-lab"></a><span data-ttu-id="caab3-110">Создание лаборатории</span><span class="sxs-lookup"><span data-stu-id="caab3-110">Create lab</span></span>

```python
async_lab = self.client.lab.create_or_update_resource(
    'MyResourceGroup',
    'MyLab',
    {'location': 'westus'}
)
lab = async_lab.result() # Blocking wait
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="caab3-111">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="caab3-111">Explore the Management APIs</span></span>](/python/api/overview/azure/devtestlabs/management)
