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
ms.openlocfilehash: 6c0bc66fbe8194b5b8f34ee8e29945b03ba8c242
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551597"
---
# <a name="service-bus-libraries-for-python"></a>Библиотеки служебной шины для Python

## <a name="overview"></a>Обзор

Служебная шина Microsoft Azure поддерживает набор облачных технологий промежуточного уровня, ориентированных на обработку сообщений. Эти технологии представлены надежными очередями сообщений, а также возможностями публикации и подписки в рамках обмена сообщениями. 

## <a name="install-the-libraries"></a>Установка библиотек
```bash
pip install azure-mgmt-servicebus
```

## <a name="servicebus-queues"></a>Очереди служебной шины
Очереди служебной шины — это альтернатива очередям хранилища. Они используются, когда требуются более сложные функции обмена сообщениями (большие размеры сообщений, упорядочение сообщений, чтение сообщений с удалением сообщений, запланированная доставка) с использованием принудительной доставки (с помощью продолжительного опроса).

Служба может использовать аутентификацию SAS или ACS.

Пространства имен служебной шины, созданные с помощью портала Azure после августа 2014 г., больше не поддерживают аутентификацию ACS. Совместимые с ACS пространства имен можно создать с помощью пакета Azure SDK.

### <a name="shared-access-signature-authentication"></a>Аутентификация SAS

Чтобы использовать аутентификацию SAS, создайте служебную шину:

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a>Аутентификация ACS

Чтобы использовать аутентификацию ACS, создайте служебную шину:

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a>Отправка и получение сообщений

Метод **create\_queue** можно использовать, чтобы проверить наличие очереди:

```python
sbs.create_queue('taskqueue')
```
Затем можно вызвать метод **send\_queue\_message**, чтобы включить сообщение в очередь:

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
После этого можно вызвать метод **send\_queue\_message_batch**, чтобы одновременно отправить несколько сообщений:

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
Также можно вызвать метод **receive\_queue\_message**, чтобы исключить сообщение из очереди.

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a>Разделы служебной шины

Разделы служебной шины — это абстракция над очередями служебной шины, которые упрощают реализацию сценариев публикации и подписки.

Метод **create\_topic** можно использовать, чтобы создать раздел на стороне сервера:

```python
sbs.create_topic('taskdiscussion')
```
Метод **send\_topic\_message** можно использовать, чтобы отправить сообщение в раздел:

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

Метод **send\_topic\_message** можно использовать, чтобы отправить несколько сообщений одновременно:

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Учтите, что строковые сообщения в Python 3 отправляются в кодировке utf-8. В Python 2 кодировкой управляет пользователь.

Клиент затем может создать подписку и начать обрабатывать сообщения, вызывая методы **create\_subscription** и **receive\_subscription\_message**. Обратите внимание на то, что все сообщения, отправленные до создания подписки, не будут получены.

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a>Концентратор событий

Концентраторы событий собирают потоки событий с высокой пропускной способностью из разнородного набора устройств и служб.

Метод **create\_event\_hub** можно использовать, чтобы создать концентратор событий:

```python
sbs.create_event_hub('myhub')
```
Отправка события

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
Содержимое событий — это сообщение о событии или строка в кодировке JSON, содержащая несколько сообщений.

## <a name="advanced-features"></a>Дополнительные функции

### <a name="broker-properties-and-user-properties"></a>Свойства Broker и User

В этом разделе описано, как использовать свойства Broker и User, определенные [здесь](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):

```python
sent_msg = Message(b'This is the third message',
                    broker_properties={'Label': 'M3'},
                    custom_properties={'Priority': 'Medium',
                                        'Customer': 'ABC'}
            )
```
Можно использовать значение даты и времени, целое число, число с плавающей запятой или логическое значение.

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
Чтобы обеспечить совместимость со старой версией этой библиотеки, `broker_properties` также можно определить как строку JSON.
В такой ситуации создавать допустимую строку JSON должен пользователь. Средства Python не будут выполнять проверку до отправки в RestAPI.

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                    broker_properties = broker_properties
)
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/servicebus/management)