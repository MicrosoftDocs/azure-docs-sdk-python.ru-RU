---
title: Библиотеки службы "Сетка событий Azure" для Python
description: ''
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
ms.openlocfilehash: e68504b3ba5834a145af1231eacc076e424a2256
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2018
---
# <a name="event-grid-libraries-for-python"></a>Библиотеки службы "Сетка событий Azure" для Python


"Сетка событий Azure" — это полностью управляемая интеллектуальная служба маршрутизации событий, которая обеспечивает равномерное потребление событий с помощью модели "публикация — подписка".

См. дополнительные сведения о [службе "Сетка событий Azure"](/azure/event-grid/overview) и начните работу с помощью [краткого руководства по событиям хранилища BLOB-объектов Azure](/azure/storage/blobs/storage-blob-event-quickstart). 

## <a name="publish-sdk"></a>Пакет SDK для публикации

Создавайте события, выполняйте аутентификацию и публикацию в разделы с помощью пакета SDK для публикации службы "Сетка событий Azure".

### <a name="installation"></a>Установка 

Установите пакет с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-eventgrid
```

### <a name="example"></a>Пример 

Следующий код публикует события в раздел. Ключ раздела и конечную точку можно получить на портале Azure или с помощью Azure CLI:

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
> [Обзор клиентских API-интерфейсов](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>Пакет SDK для управления

Создавайте, обновляйте и удаляйте экземпляры, разделы и подписки службы "Сетка событий" с помощью пакета SDK для управления.

### <a name="installation"></a>Установка 

Установите пакет с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>Пример

В следующем примере создается пользовательский раздел и подписка на раздел для конечной точки. Затем код отправляет событие в раздел по протоколу HTTPS.
RequestBin является сторонним средством с открытым кодом, позволяющим создать конечную точку и просматривать запросы, отправленные на нее. Последовательно выберите пункты [RequestBin](https://requestb.in/)и щелкните **Создать RequestBin**. Скопируйте URL-адрес ячейки, так как он понадобится при подписке на тему.

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
Перейдите по URL-адресу RequestBin, созданному ранее, чтобы увидеть отправленное событие.

Очистка ресурсов
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>Подробнее

[Получение событий с помощью пакета SDK службы "Сетка событий"](/azure/event-grid/receive-events)