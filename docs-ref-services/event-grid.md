---
title: "Библиотеки службы \"Сетка событий Azure\" для Python"
description: 
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: 299b50ce8366d0c49ade28dfece98d6696a4f9ef
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="344ea-103">Библиотеки службы "Сетка событий Azure" для Python</span><span class="sxs-lookup"><span data-stu-id="344ea-103">Event Grid libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="344ea-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="344ea-104">Overview</span></span>
<span data-ttu-id="344ea-105">"Сетка событий Azure" — это полностью управляемая интеллектуальная служба маршрутизации событий, которая обеспечивает равномерное потребление событий с помощью модели "публикация — подписка".</span><span class="sxs-lookup"><span data-stu-id="344ea-105">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

## <a name="management-api"></a><span data-ttu-id="344ea-106">API управления</span><span class="sxs-lookup"><span data-stu-id="344ea-106">Management API</span></span>
```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="344ea-107">Пример</span><span class="sxs-lookup"><span data-stu-id="344ea-107">Example</span></span>
<span data-ttu-id="344ea-108">В следующем примере создается пользовательский раздел и подписка на раздел, а затем активируется событие для просмотра результатов.</span><span class="sxs-lookup"><span data-stu-id="344ea-108">The following creates a custom topic, subscribes to the topic, and triggers the event to view the result.</span></span> <span data-ttu-id="344ea-109">RequestBin является сторонним средством с открытым кодом, позволяющим создать конечную точку и просматривать запросы, отправленные на нее.</span><span class="sxs-lookup"><span data-stu-id="344ea-109">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="344ea-110">Последовательно выберите пункты [RequestBin](https://requestb.in/)и щелкните **Создать RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="344ea-110">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="344ea-111">Скопируйте URL-адрес ячейки, так как он понадобится при подписке на тему.</span><span class="sxs-lookup"><span data-stu-id="344ea-111">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.eventgrid import EventGridManagementClient
import requests

RESOURCE_GROUP_NAME = 'gridResourceGroup'
TOPIC_NAME = 'gridTopic1234'
LOCATION = 'westus2'
SUBSCRIPTION_ID = 'YOUR_SUBSCRIPTION_ID'
SUBSCRIPTION_NAME = 'gridSubscription'
REQUEST_BIN_URL = 'YOUR_REQUEST_BIN_URL'

# create resource group
resource_client = ResourceManagementClient(credentials, SUBSCRIPTION_ID)
resource_client.resource_groups.create_or_update(
    RESOURCE_GROUP_NAME,
    {
        'location': LOCATION
    }
)

event_client = EventGridManagementClient(credentials, SUBSCRIPTION_ID)

# create a custom topic
event_client.topics.create_or_update(RESOURCE_GROUP_NAME, TOPIC_NAME, LOCATION)

# subscribe to a topic
scope = '/subscriptions/'+SUBSCRIPTION_ID+'/resourceGroups/'+RESOURCE_GROUP_NAME+'/providers/Microsoft.EventGrid/topics/'+TOPIC_NAME
event_client.event_subscriptions.create(scope, SUBSCRIPTION_NAME,
    {
        'destination': {
            'endpoint_url': REQUEST_BIN_URL
        }
    }
)

# send an event to topic
# get endpoint url
url = event_client.event_subscriptions.get_full_url(scope, SUBSCRIPTION_NAME).endpoint_url
# get key
key = event_client.topics.list_shared_access_keys(RESOURCE_GROUP_NAME,TOPIC_NAME).key1
headers = {'aeg-sas-key': key}
s = requests.get('https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json')
r = requests.post(url, data=s, headers=headers)
print(r.status_code)
print(r.content)
```
<span data-ttu-id="344ea-112">Перейдите по URL-адресу RequestBin, созданному ранее, чтобы увидеть отправленное событие.</span><span class="sxs-lookup"><span data-stu-id="344ea-112">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="344ea-113">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="344ea-113">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="344ea-114">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="344ea-114">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

