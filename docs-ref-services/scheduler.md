---
title: "Библиотеки планировщика Azure для Python"
description: "Справочник по библиотекам планировщика Azure для Python"
keywords: Azure, python, SDK, API, Scheduler
author: lisawong19
ms.author: liwong
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 3d2691ae1ba84c41f25de2b099aacefaa92152ed
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/24/2018
---
# <a name="azure-scheduler-libraries-for-python"></a><span data-ttu-id="873e2-104">Библиотеки планировщика Azure для Python</span><span class="sxs-lookup"><span data-stu-id="873e2-104">Azure Scheduler libraries for python</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="873e2-105">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="873e2-105">Install the libraries</span></span>

## <a name="management"></a><span data-ttu-id="873e2-106">управления</span><span class="sxs-lookup"><span data-stu-id="873e2-106">Management</span></span>

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a><span data-ttu-id="873e2-107">Пример</span><span class="sxs-lookup"><span data-stu-id="873e2-107">Example</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="873e2-108">Создание клиента управления</span><span class="sxs-lookup"><span data-stu-id="873e2-108">Create the management client</span></span>

<span data-ttu-id="873e2-109">Следующий код создает экземпляр клиента управления.</span><span class="sxs-lookup"><span data-stu-id="873e2-109">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="873e2-110">Вам нужно указать ваш ``subscription_id``, который можно получить в [списке подписок](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="873e2-110">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="873e2-111">Дополнительные сведения об аутентификации Azure Active Directory с помощью пакета SDK Python и создании экземпляра ``Credentials`` см. в руководстве по [аутентификации управления ресурсами](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="873e2-111">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.scheduler import SchedulerManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

scheduler_client = SchedulerManagementClient(
    credentials,
    subscription_id
)
```

### <a name="create-a-job-collection"></a><span data-ttu-id="873e2-112">Создание коллекции заданий</span><span class="sxs-lookup"><span data-stu-id="873e2-112">Create a job collection</span></span>

<span data-ttu-id="873e2-113">Этот пример создает коллекцию заданий в существующей группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="873e2-113">The following code creates a job collection under an existing resource group.</span></span>
<span data-ttu-id="873e2-114">См. дополнительные сведения о [создании групп ресурсов и управлении ими](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="873e2-114">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.scheduler.models import JobCollectionDefinition, JobCollectionProperties, Sku

group_name = 'myresourcegroup'
job_collection_name = "myjobcollection"
scheduler_client.job_collections.create_or_update(
    group_name,
    job_collection_name,
    JobCollectionDefinition(
        location = "West US",
        properties = JobCollectionProperties(
            sku = Sku(
                name="Free"
            )
        )
    )
)
# scheduler_client is a JobCollectionDefinition instance
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="873e2-115">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="873e2-115">Explore the Management APIs</span></span>](/python/api/overview/azure/scheduler/management)