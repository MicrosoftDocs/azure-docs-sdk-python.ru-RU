---
title: Библиотеки служебной шины для Python
description: Справочная документация по клиентским библиотекам и библиотекам управления служебной шины для Python
keywords: Azure, Python, SDK, API, messaging, pubsub, pub-sub, message broker
author: annatisch
ms.author: antisch
manager: mayurid
ms.date: 01/15/2019
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 540a2a248f7a2abcc83517bc4a4ef96ef03e8a9f
ms.sourcegitcommit: fba77bdf8eb9f49621be94544d9fef88aff98c14
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747744"
---
# <a name="service-bus-libraries-for-python"></a>Библиотеки служебной шины для Python

Служебная шина Microsoft Azure поддерживает набор облачных технологий промежуточного уровня, ориентированных на обработку сообщений. Эти технологии представлены надежными очередями сообщений, а также возможностями публикации и подписки в рамках обмена сообщениями.

* [Исходный код пакета SDK](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [Справочная документация по пакету SDK](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a>Новые возможности версии 0.50.0
Начиная с версии 0.50.0, новый API на основе AMQP можно использовать для отправки и получения сообщений. Это обновление включает в себя **критические изменения**.
Чтобы узнать, подходит ли для вас сейчас обновление, см. руководство по [переходу с версии 0.21.1 на версию 0.50.0](#migration-from-v0211-to-v0500).

Новое предложение API на основе AMQP предлагает надежную передачу сообщений, высокую производительность и расширенную поддержку соответствующих возможностей в будущем.
Новое предложение API также поддерживает асинхронные операции (на основе asyncio) для отправки, получения и обработки сообщений.

См. дополнительные сведения об [операциях на основе HTTP с использованием устаревшего API](#using-http-based-operations-of-the-legacy-api).


## <a name="prerequisites"></a>Предварительные требования

* Подписка Azure — [создайте бесплатную учетную запись](https://azure.microsoft.com/free/).
* [Учетные данные для управления и пространство имен служебной шины](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal) Azure.
* [Python 2.7–3.7](https://www.python.org/downloads/).


## <a name="installation"></a>Установка
```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a>Подключение к служебной шине Azure

### <a name="get-credentials"></a>Получение учетных данных
Используйте приведенный ниже фрагмент кода Azure CLI для заполнения переменной среды строкой подключения служебной шины (вы можете найти это значение на портале Azure). Фрагмент кода отформатирован для оболочки Bash.

```Bash
RES_GROUP=<resource-group-name>
NAMESPACE=<servicebus-namespace>

export SB_CONN_STR=$(az servicebus namespace authorization-rule keys list \
 --resource-group $RES_GROUP \
 --namespace-name $NAMESPACE \
 --name RootManageSharedAccessKey \
 --query primaryConnectionString \
 --output tsv)
```

### <a name="create-client"></a>Создание клиента
Когда вы заполните переменную среды `SB_CONN_STR`, создайте ServiceBusClient.
```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```
Если вы хотите выполнять асинхронные операции, используйте пространство имен `azure.servicebus.aio`.
```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```


## <a name="service-bus-queues"></a>Очереди служебной шины
Очереди служебной шины — это альтернатива очередям хранилища. Они используются, когда требуются более сложные функции обмена сообщениями (обработка сообщений большиих размеров, упорядочение сообщений, чтение сообщений с удалением сообщений, запланированная доставка) с использованием принудительной доставки (с помощью продолжительного опроса).

### <a name="create-queue"></a>Создание очереди
Вы можете создать очередь в пространстве имен служебной шины. Если очередь с тем же именем уже существует в пространстве имен, возникает ошибка. 
```python
sb_client.create_queue("MyQueue")
```
Также можно указать необязательные параметры, чтобы настроить поведение очереди.
```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a>Получение клиента очереди
QueueClient можно использовать для обмена сообщениями в очереди, а также других операций.
```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a>Отправка сообщений
Клиент очереди может отправлять одно или несколько сообщений одновременно.
```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```
Каждый вызов к QueueClient.send создает новое подключение к службе. Чтобы повторно использовать одно подключение для нескольких вызовов отправки, можно открыть отправителя.
```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```
При использовании асинхронного клиента, в указанных выше операциях используется синтаксис async.
```python
from azure.servicebus.aio import Message

message = Message("Hello World")
await queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
async with queue_client.get_sender() as sender:
    await sender.send(message_one)
    await sender.send(message_two)
```


### <a name="receiving-messages"></a>Получение сообщений
Сообщения можно получать из очереди в рамках цикла непрерывной итерации. Режим по умолчанию для приема сообщений — [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read). Для включения этого режима требуется, чтобы каждое сообщение было явно завершено для его удаления из очереди.
```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```
Подключение службы будет оставаться открытым на протяжении всего цикла итерации.
Если для потока сообщений выполняется только частичная итерация, запустите получатель в операторе `with`, чтобы закрыть подключение.
```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
При использовании асинхронного клиента, в указанных выше операциях используется синтаксис async.
```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a>Разделы и подписки служебной шины

Наряду с очередями служебной шины разделы и подписки служебной шины представляют еще один уровень абстракции. Эти сущности обеспечивают разновидность взаимодействия "один ко многим" в рамках схемы публикации и подписки. Сообщения отправляются в раздел и доставляются в одну или несколько связанных подписок. Это особенно удобно при масштабировании с учетом большого количества получателей.

### <a name="create-topic"></a>Создание раздела
Вы можете создать раздел в пространстве имен служебной шины. Если раздел с тем же именем уже существует, возникает ошибка. 
```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a>Получение клиента раздела
TopicClient можно использовать для отправки сообщений в раздел, а также других операций.
```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a>Создание подписки
Вы можете создать подписку для указанного раздела в пространстве имен служебной шины.
```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a>Получение клиента подписки
SubscriptionClient можно использовать для получения сообщений из раздела, а также других операций.
```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a>Переход с версии 0.21.1 на версию 0.50.0
В версии 0.50.0 представлены основные критические изменения.
Исходный API на основе HTTP по-прежнему доступен в версии 0.50.0, но теперь он включен в новое пространство имен: `azure.servicebus.control_client`.

### <a name="should-i-upgrade"></a>Следует ли выполнять обновление?
Новый пакет (версии 0.50.0) не включает улучшения операций на основе HTTP в сравнении с версией 0.21.1. API на основе HTTP является идентичным, за исключением того, что этот интерфейс включен в новое пространство имен. Поэтому, если вы хотите использовать операции на основе HTTP (`create_queue`, `delete_queue` и т.д.), сейчас вы не получите дополнительные преимущества от обновления.


### <a name="how-do-i-migrate-my-code-to-the-new-version"></a>Как перенести код в новую версию?
Код, написанный для версии 0.21.0, можно перенести в версию 0.50.0. Для этого нужно просто изменить пространство имен для импорта.

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a>Использование операций на основе HTTP в устаревшей версии API
В следующей документации описана устаревшая версия API. Она предназначена для тех, кто хочет перенести существующий код в версию 0.50.0 без внесения дополнительных изменений. Эти справочные материалы также можно использовать как рекомендации для пользователей версии 0.21.1.
Для тех, кто создает новый код, мы рекомендуем использовать новый API, описанный выше.

### <a name="service-bus-queues"></a>Очереди служебной шины

#### <a name="shared-access-signature-sas-authentication"></a>Аутентификация SAS

Чтобы использовать аутентификацию SAS, создайте служебную шину:

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a>Аутентификация службы контроля доступа (ACS)
ACS не поддерживается в новом пространстве имен служебной шины. Мы рекомендуем [перенести приложения для использования аутентификации SAS](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).
Чтобы использовать аутентификацию ACS в предыдущем пространстве имен служебной шины, создайте ServiceBusService:

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
#### <a name="sending-and-receiving-messages"></a>Отправка и получение сообщений

Метод **create\_queue** можно использовать, чтобы проверить наличие очереди:

```python
sbs.create_queue('taskqueue')
```
Затем можно вызвать метод **send\_queue\_message**, чтобы включить сообщение в очередь:

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
После этого можно вызвать метод **send\_queue\_message_batch**, чтобы одновременно отправить несколько сообщений:

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
Также можно вызвать метод **receive\_queue\_message**, чтобы исключить сообщение из очереди.

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a>Разделы служебной шины

Метод **create\_topic** можно использовать, чтобы создать раздел на стороне сервера:

```python
sbs.create_topic('taskdiscussion')
```
Метод **send\_topic\_message** можно использовать, чтобы отправить сообщение в раздел:

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

Метод **send\_topic\_message** можно использовать, чтобы отправить несколько сообщений одновременно:

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Учтите, что строковые сообщения в Python 3 отправляются в кодировке utf-8. В Python 2 кодировкой управляет пользователь.

Клиент затем может создать подписку и начать обрабатывать сообщения, вызывая методы **create\_subscription** и **receive\_subscription\_message**. Обратите внимание на то, что все сообщения, отправленные до создания подписки, не будут получены.

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a>Концентратор событий

Центры событий собирают потоки событий с высокой пропускной способностью из разнородного набора устройств и служб.

Метод **create\_event\_hub** можно использовать, чтобы создать концентратор событий:

```python
sbs.create_event_hub('myhub')
```
Отправка события

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
Содержимое событий — это сообщение о событии или строка в кодировке JSON, содержащая несколько сообщений.

### <a name="advanced-features"></a>Дополнительные функции

#### <a name="broker-properties-and-user-properties"></a>Свойства Broker и User

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

## <a name="next-steps"></a>Дальнейшие действия
* [Документация по служебной шине](https://docs.microsoft.com/azure/service-bus-messaging)
* [Исходный код пакета SDK](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [Справочная документация по пакету SDK](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [Дополнительные примеры](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
