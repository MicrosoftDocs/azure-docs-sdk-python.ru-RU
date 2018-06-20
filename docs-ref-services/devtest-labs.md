---
title: Библиотеки Azure DevTest Labs для Python
description: Справочник по библиотекам Azure DevTest Labs для Python
keywords: Azure, python, SDK, API, DevTest Labs
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 5807b85f02c05c2a767a2df2e89d9e98b7e6e05b
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551577"
---
# <a name="azure-devtest-labs-libraries-for-python"></a>Библиотеки Azure DevTest Labs для Python

## <a name="management-apipythonapioverviewazuredevtestlabsmanagement"></a>[API управления](/python/api/overview/azure/devtestlabs/management)

```bash
pip install azure-mgmt-devtestlabs
```

## <a name="create-the-management-client"></a>Создание клиента управления

Следующий код создает экземпляр клиента управления.

Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).

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

## <a name="create-lab"></a>Создание лаборатории

```python
async_lab = self.client.lab.create_or_update_resource(
    'MyResourceGroup',
    'MyLab',
    {'location': 'westus'}
)
lab = async_lab.result() # Blocking wait
``` 

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/devtestlabs/management)