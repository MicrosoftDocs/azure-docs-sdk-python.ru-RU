---
title: Библиотеки службы "Сетка событий Azure" для Python
description: ''
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: bfaa1908295eb77531e399f1337acdeee512005f
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276838"
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="cb425-103">Библиотеки службы "Сетка событий Azure" для Python</span><span class="sxs-lookup"><span data-stu-id="cb425-103">Event Grid libraries for Python</span></span>


<span data-ttu-id="cb425-104">"Сетка событий Azure" — это полностью управляемая интеллектуальная служба маршрутизации событий, которая обеспечивает равномерное потребление событий с помощью модели "публикация — подписка".</span><span class="sxs-lookup"><span data-stu-id="cb425-104">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

<span data-ttu-id="cb425-105">См. дополнительные сведения о [службе "Сетка событий Azure"](/azure/event-grid/overview) и начните работу с помощью [краткого руководства по событиям хранилища BLOB-объектов Azure](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="cb425-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="cb425-106">Пакет SDK для публикации</span><span class="sxs-lookup"><span data-stu-id="cb425-106">Publish SDK</span></span>

<span data-ttu-id="cb425-107">Создавайте события, выполняйте аутентификацию и публикацию в разделы с помощью пакета SDK для публикации службы "Сетка событий Azure".</span><span class="sxs-lookup"><span data-stu-id="cb425-107">Authenticate, create, handle, and publish events to topics using the Azure Event Grid publish SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="cb425-108">Установка</span><span class="sxs-lookup"><span data-stu-id="cb425-108">Installation</span></span> 

<span data-ttu-id="cb425-109">Установите пакет с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="cb425-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-eventgrid
```

### <a name="example"></a><span data-ttu-id="cb425-110">Пример</span><span class="sxs-lookup"><span data-stu-id="cb425-110">Example</span></span> 

<span data-ttu-id="cb425-111">Следующий код публикует события в раздел.</span><span class="sxs-lookup"><span data-stu-id="cb425-111">The following code publishes an event to a topic.</span></span> <span data-ttu-id="cb425-112">Ключ раздела и конечную точку можно получить на портале Azure или с помощью Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="cb425-112">You can retrieve the topic key and endpoint through the Azure Portal or through the Azure CLI:</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

```python
from datetime import datetime
from azure.eventgrid import EventGridClient
from msrest.authentication import TopicCredentials

def publish_event(self):

        credentials = TopicCredentials(
            self.settings.EVENT_GRID_KEY
        )
        event_grid_client = EventGridClient(credentials)
        event_grid_client.publish_events(
            "your-endpoint-here",
            events=[{
                'id' : "dbf93d79-3859-4cac-8055-51e3b6b54bea",
                'subject' : "Sample subject",
                'data': {
                    'key': 'Sample Data'
                },
                'event_type': 'SampleEventType',
                'event_time': datetime(2018, 5, 2),
                'data_version': 1
            }]
        )
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb425-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="cb425-113">Explore the Client APIs</span></span>](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="cb425-114">Пакет SDK для управления</span><span class="sxs-lookup"><span data-stu-id="cb425-114">Management SDK</span></span>

<span data-ttu-id="cb425-115">Создавайте, обновляйте и удаляйте экземпляры, разделы и подписки службы "Сетка событий" с помощью пакета SDK для управления.</span><span class="sxs-lookup"><span data-stu-id="cb425-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="cb425-116">Установка</span><span class="sxs-lookup"><span data-stu-id="cb425-116">Installation</span></span> 

<span data-ttu-id="cb425-117">Установите пакет с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="cb425-117">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="cb425-118">Пример</span><span class="sxs-lookup"><span data-stu-id="cb425-118">Example</span></span>

<span data-ttu-id="cb425-119">В следующем примере создается пользовательский раздел и подписка на раздел для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="cb425-119">The following creates a custom topic and subscribes an endpoint to the topic.</span></span> <span data-ttu-id="cb425-120">Затем код отправляет событие в раздел по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cb425-120">The code then sends an event to the topic through HTTPS.</span></span>
<span data-ttu-id="cb425-121">RequestBin является сторонним средством с открытым кодом, позволяющим создать конечную точку и просматривать запросы, отправленные на нее.</span><span class="sxs-lookup"><span data-stu-id="cb425-121">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="cb425-122">Последовательно выберите пункты [RequestBin](https://requestb.in/)и щелкните **Создать RequestBin**.</span><span class="sxs-lookup"><span data-stu-id="cb425-122">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="cb425-123">Скопируйте URL-адрес ячейки, так как он понадобится при подписке на тему.</span><span class="sxs-lookup"><span data-stu-id="cb425-123">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="cb425-124">Перейдите по URL-адресу RequestBin, созданному ранее, чтобы увидеть отправленное событие.</span><span class="sxs-lookup"><span data-stu-id="cb425-124">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="cb425-125">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="cb425-125">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb425-126">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="cb425-126">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="cb425-127">Подробнее</span><span class="sxs-lookup"><span data-stu-id="cb425-127">Learn more</span></span>

[<span data-ttu-id="cb425-128">Получение событий с помощью пакета SDK службы "Сетка событий"</span><span class="sxs-lookup"><span data-stu-id="cb425-128">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)
