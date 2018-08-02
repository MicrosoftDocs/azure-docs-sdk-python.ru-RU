---
title: Библиотеки служебной шины для Python
description: Справочная документация по клиентским библиотекам и библиотекам управления служебной шины для Python
keywords: Azure, Python, SDK, API, messaging, pubsub, pub-sub, message broker
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 02c172ff1a54d060c6af36a5a5daa5dcbff8795c
ms.sourcegitcommit: e35ec475d4b9d8061d0528a93aa8e1c4b7db6c0d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/02/2018
ms.locfileid: "39418959"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="09666-104">Библиотеки служебной шины для Python</span><span class="sxs-lookup"><span data-stu-id="09666-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="09666-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="09666-105">Overview</span></span>

<span data-ttu-id="09666-106">Служебная шина Microsoft Azure поддерживает набор облачных технологий промежуточного уровня, ориентированных на обработку сообщений. Эти технологии представлены надежными очередями сообщений, а также возможностями публикации и подписки в рамках обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="09666-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="09666-107">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="09666-107">Install the libraries</span></span>
```bash
pip install azure-servicebus
```

## <a name="servicebus-queues"></a><span data-ttu-id="09666-108">Очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="09666-108">ServiceBus Queues</span></span>
<span data-ttu-id="09666-109">Очереди служебной шины — это альтернатива очередям хранилища. Они используются, когда требуются более сложные функции обмена сообщениями (большие размеры сообщений, упорядочение сообщений, чтение сообщений с удалением сообщений, запланированная доставка) с использованием принудительной доставки (с помощью продолжительного опроса).</span><span class="sxs-lookup"><span data-stu-id="09666-109">ServiceBus Queues are an alternative to Storage Queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

<span data-ttu-id="09666-110">Служба может использовать аутентификацию SAS или ACS.</span><span class="sxs-lookup"><span data-stu-id="09666-110">The service can use Shared Access Signature authentication, or ACS authentication.</span></span>

<span data-ttu-id="09666-111">Пространства имен служебной шины, созданные с помощью портала Azure после августа 2014 г., больше не поддерживают аутентификацию ACS.</span><span class="sxs-lookup"><span data-stu-id="09666-111">Service bus namespaces created using the Azure portal after August 2014 no longer support ACS authentication.</span></span> <span data-ttu-id="09666-112">Совместимые с ACS пространства имен можно создать с помощью пакета Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="09666-112">You can create ACS compatible namespaces with the Azure SDK.</span></span>

### <a name="shared-access-signature-authentication"></a><span data-ttu-id="09666-113">Аутентификация SAS</span><span class="sxs-lookup"><span data-stu-id="09666-113">Shared Access Signature Authentication</span></span>

<span data-ttu-id="09666-114">Чтобы использовать аутентификацию SAS, создайте служебную шину:</span><span class="sxs-lookup"><span data-stu-id="09666-114">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a><span data-ttu-id="09666-115">Аутентификация ACS</span><span class="sxs-lookup"><span data-stu-id="09666-115">ACS Authentication</span></span>

<span data-ttu-id="09666-116">Чтобы использовать аутентификацию ACS, создайте служебную шину:</span><span class="sxs-lookup"><span data-stu-id="09666-116">To use ACS authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a><span data-ttu-id="09666-117">Отправка и получение сообщений</span><span class="sxs-lookup"><span data-stu-id="09666-117">Sending and Receiving Messages</span></span>

<span data-ttu-id="09666-118">Метод **create\_queue** можно использовать, чтобы проверить наличие очереди:</span><span class="sxs-lookup"><span data-stu-id="09666-118">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="09666-119">Затем можно вызвать метод **send\_queue\_message**, чтобы включить сообщение в очередь:</span><span class="sxs-lookup"><span data-stu-id="09666-119">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="09666-120">После этого можно вызвать метод **send\_queue\_message_batch**, чтобы одновременно отправить несколько сообщений:</span><span class="sxs-lookup"><span data-stu-id="09666-120">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="09666-121">Также можно вызвать метод **receive\_queue\_message**, чтобы исключить сообщение из очереди.</span><span class="sxs-lookup"><span data-stu-id="09666-121">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a><span data-ttu-id="09666-122">Разделы служебной шины</span><span class="sxs-lookup"><span data-stu-id="09666-122">ServiceBus Topics</span></span>

<span data-ttu-id="09666-123">Разделы служебной шины — это абстракция над очередями служебной шины, которые упрощают реализацию сценариев публикации и подписки.</span><span class="sxs-lookup"><span data-stu-id="09666-123">ServiceBus topics are an abstraction on top of ServiceBus Queues that make pub/sub scenarios easy to implement.</span></span>

<span data-ttu-id="09666-124">Метод **create\_topic** можно использовать, чтобы создать раздел на стороне сервера:</span><span class="sxs-lookup"><span data-stu-id="09666-124">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="09666-125">Метод **send\_topic\_message** можно использовать, чтобы отправить сообщение в раздел:</span><span class="sxs-lookup"><span data-stu-id="09666-125">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="09666-126">Метод **send\_topic\_message** можно использовать, чтобы отправить несколько сообщений одновременно:</span><span class="sxs-lookup"><span data-stu-id="09666-126">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="09666-127">Учтите, что строковые сообщения в Python 3 отправляются в кодировке utf-8. В Python 2 кодировкой управляет пользователь.</span><span class="sxs-lookup"><span data-stu-id="09666-127">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="09666-128">Клиент затем может создать подписку и начать обрабатывать сообщения, вызывая методы **create\_subscription** и **receive\_subscription\_message**.</span><span class="sxs-lookup"><span data-stu-id="09666-128">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="09666-129">Обратите внимание на то, что все сообщения, отправленные до создания подписки, не будут получены.</span><span class="sxs-lookup"><span data-stu-id="09666-129">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a><span data-ttu-id="09666-130">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="09666-130">Event Hub</span></span>

<span data-ttu-id="09666-131">Концентраторы событий собирают потоки событий с высокой пропускной способностью из разнородного набора устройств и служб.</span><span class="sxs-lookup"><span data-stu-id="09666-131">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="09666-132">Метод **create\_event\_hub** можно использовать, чтобы создать концентратор событий:</span><span class="sxs-lookup"><span data-stu-id="09666-132">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="09666-133">Отправка события</span><span class="sxs-lookup"><span data-stu-id="09666-133">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="09666-134">Содержимое событий — это сообщение о событии или строка в кодировке JSON, содержащая несколько сообщений.</span><span class="sxs-lookup"><span data-stu-id="09666-134">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

## <a name="advanced-features"></a><span data-ttu-id="09666-135">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="09666-135">Advanced features</span></span>

### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="09666-136">Свойства Broker и User</span><span class="sxs-lookup"><span data-stu-id="09666-136">Broker Properties and User Properties</span></span>

<span data-ttu-id="09666-137">В этом разделе описано, как использовать свойства Broker и User, определенные [здесь](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span><span class="sxs-lookup"><span data-stu-id="09666-137">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                    broker_properties={'Label': 'M3'},
                    custom_properties={'Priority': 'Medium',
                                        'Customer': 'ABC'}
            )
```
<span data-ttu-id="09666-138">Можно использовать значение даты и времени, целое число, число с плавающей запятой или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="09666-138">You can use datetime, int, float or boolean</span></span>

```python
props = {'hello': 'world',
            'number': 42,
            'active': True,
            'deceased': False,
            'large': 8555111000,
            'floating': 3.14,
            'dob': datetime(2011, 12, 14),
            'double_quote_message': 'This "should" work fine',
            'quote_message': "This 'should' work fine"}
sent_msg = Message(b'message with properties', custom_properties=props)
```
<span data-ttu-id="09666-139">Чтобы обеспечить совместимость со старой версией этой библиотеки, `broker_properties` также можно определить как строку JSON.</span><span class="sxs-lookup"><span data-stu-id="09666-139">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="09666-140">В такой ситуации создавать допустимую строку JSON должен пользователь. Средства Python не будут выполнять проверку до отправки в RestAPI.</span><span class="sxs-lookup"><span data-stu-id="09666-140">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                    broker_properties = broker_properties
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="09666-141">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="09666-141">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/management)
