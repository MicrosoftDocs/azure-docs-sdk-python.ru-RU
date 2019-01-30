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
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="ae524-104">Библиотеки служебной шины для Python</span><span class="sxs-lookup"><span data-stu-id="ae524-104">Service Bus libraries for Python</span></span>

<span data-ttu-id="ae524-105">Служебная шина Microsoft Azure поддерживает набор облачных технологий промежуточного уровня, ориентированных на обработку сообщений. Эти технологии представлены надежными очередями сообщений, а также возможностями публикации и подписки в рамках обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="ae524-105">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span>

* [<span data-ttu-id="ae524-106">Исходный код пакета SDK</span><span class="sxs-lookup"><span data-stu-id="ae524-106">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="ae524-107">Справочная документация по пакету SDK</span><span class="sxs-lookup"><span data-stu-id="ae524-107">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a><span data-ttu-id="ae524-108">Новые возможности версии 0.50.0</span><span class="sxs-lookup"><span data-stu-id="ae524-108">What's new in v0.50.0?</span></span>
<span data-ttu-id="ae524-109">Начиная с версии 0.50.0, новый API на основе AMQP можно использовать для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="ae524-109">As of version 0.50.0 a new AMQP-based API is available for sending and receiving messages.</span></span> <span data-ttu-id="ae524-110">Это обновление включает в себя **критические изменения**.</span><span class="sxs-lookup"><span data-stu-id="ae524-110">This update involves **breaking changes**.</span></span>
<span data-ttu-id="ae524-111">Чтобы узнать, подходит ли для вас сейчас обновление, см. руководство по [переходу с версии 0.21.1 на версию 0.50.0](#migration-from-v0211-to-v0500).</span><span class="sxs-lookup"><span data-stu-id="ae524-111">Please read [Migration from v0.21.1 to v0.50.0](#migration-from-v0211-to-v0500) to determine if upgrading is right for you at this time.</span></span>

<span data-ttu-id="ae524-112">Новое предложение API на основе AMQP предлагает надежную передачу сообщений, высокую производительность и расширенную поддержку соответствующих возможностей в будущем.</span><span class="sxs-lookup"><span data-stu-id="ae524-112">The new AMQP-based API offers improved message passing reliability, performance and expanded feature support going forward.</span></span>
<span data-ttu-id="ae524-113">Новое предложение API также поддерживает асинхронные операции (на основе asyncio) для отправки, получения и обработки сообщений.</span><span class="sxs-lookup"><span data-stu-id="ae524-113">The new API also offers support for asynchronous operations (based on asyncio) for sending, receiving and handling messages.</span></span>

<span data-ttu-id="ae524-114">См. дополнительные сведения об [операциях на основе HTTP с использованием устаревшего API](#using-http-based-operations-of-the-legacy-api).</span><span class="sxs-lookup"><span data-stu-id="ae524-114">For documentation on the legacy HTTP-based operations please see [Using HTTP-based operations of the legacy API](#using-http-based-operations-of-the-legacy-api).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ae524-115">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae524-115">Prerequisites</span></span>

* <span data-ttu-id="ae524-116">Подписка Azure — [создайте бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ae524-116">Azure subscription - [Create a free account](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="ae524-117">[Учетные данные для управления и пространство имен служебной шины](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal) Azure.</span><span class="sxs-lookup"><span data-stu-id="ae524-117">Azure [Service Bus namespace and management credentials](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span></span>
* <span data-ttu-id="ae524-118">[Python 2.7–3.7](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ae524-118">[Python 2.7-3.7](https://www.python.org/downloads/)</span></span>


## <a name="installation"></a><span data-ttu-id="ae524-119">Установка</span><span class="sxs-lookup"><span data-stu-id="ae524-119">Installation</span></span>
```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a><span data-ttu-id="ae524-120">Подключение к служебной шине Azure</span><span class="sxs-lookup"><span data-stu-id="ae524-120">Connect to Azure Service Bus</span></span>

### <a name="get-credentials"></a><span data-ttu-id="ae524-121">Получение учетных данных</span><span class="sxs-lookup"><span data-stu-id="ae524-121">Get credentials</span></span>
<span data-ttu-id="ae524-122">Используйте приведенный ниже фрагмент кода Azure CLI для заполнения переменной среды строкой подключения служебной шины (вы можете найти это значение на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="ae524-122">Use the Azure CLI snippet below to populate an environment variable with the Service Bus connection string (you can also find this value in the Azure portal).</span></span> <span data-ttu-id="ae524-123">Фрагмент кода отформатирован для оболочки Bash.</span><span class="sxs-lookup"><span data-stu-id="ae524-123">The snippet is formatted for the Bash shell.</span></span>

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

### <a name="create-client"></a><span data-ttu-id="ae524-124">Создание клиента</span><span class="sxs-lookup"><span data-stu-id="ae524-124">Create client</span></span>
<span data-ttu-id="ae524-125">Когда вы заполните переменную среды `SB_CONN_STR`, создайте ServiceBusClient.</span><span class="sxs-lookup"><span data-stu-id="ae524-125">Once you've populated the `SB_CONN_STR` environment variable, you can create the ServiceBusClient.</span></span>
```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```
<span data-ttu-id="ae524-126">Если вы хотите выполнять асинхронные операции, используйте пространство имен `azure.servicebus.aio`.</span><span class="sxs-lookup"><span data-stu-id="ae524-126">If you wish to use asynchronous operations, please use the `azure.servicebus.aio` namespace.</span></span>
```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```


## <a name="service-bus-queues"></a><span data-ttu-id="ae524-127">Очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="ae524-127">Service Bus queues</span></span>
<span data-ttu-id="ae524-128">Очереди служебной шины — это альтернатива очередям хранилища. Они используются, когда требуются более сложные функции обмена сообщениями (обработка сообщений большиих размеров, упорядочение сообщений, чтение сообщений с удалением сообщений, запланированная доставка) с использованием принудительной доставки (с помощью продолжительного опроса).</span><span class="sxs-lookup"><span data-stu-id="ae524-128">Service Bus queues are an alternative to Storage queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

### <a name="create-queue"></a><span data-ttu-id="ae524-129">Создание очереди</span><span class="sxs-lookup"><span data-stu-id="ae524-129">Create queue</span></span>
<span data-ttu-id="ae524-130">Вы можете создать очередь в пространстве имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="ae524-130">This creates a new queue within the Service Bus namespace.</span></span> <span data-ttu-id="ae524-131">Если очередь с тем же именем уже существует в пространстве имен, возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="ae524-131">If a queue of the same name already exists within the namespace an error will be raised.</span></span> 
```python
sb_client.create_queue("MyQueue")
```
<span data-ttu-id="ae524-132">Также можно указать необязательные параметры, чтобы настроить поведение очереди.</span><span class="sxs-lookup"><span data-stu-id="ae524-132">Optional parameters to configure the queue behaviour can also be specified.</span></span>
```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a><span data-ttu-id="ae524-133">Получение клиента очереди</span><span class="sxs-lookup"><span data-stu-id="ae524-133">Get a queue client</span></span>
<span data-ttu-id="ae524-134">QueueClient можно использовать для обмена сообщениями в очереди, а также других операций.</span><span class="sxs-lookup"><span data-stu-id="ae524-134">A QueueClient can be used to send and receive messages from the queue, along with other operations.</span></span>
```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a><span data-ttu-id="ae524-135">Отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="ae524-135">Sending messages</span></span>
<span data-ttu-id="ae524-136">Клиент очереди может отправлять одно или несколько сообщений одновременно.</span><span class="sxs-lookup"><span data-stu-id="ae524-136">The queue client can send one or more messages at a time:</span></span>
```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```
<span data-ttu-id="ae524-137">Каждый вызов к QueueClient.send создает новое подключение к службе.</span><span class="sxs-lookup"><span data-stu-id="ae524-137">Each call to QueueClient.send will create a new service connection.</span></span> <span data-ttu-id="ae524-138">Чтобы повторно использовать одно подключение для нескольких вызовов отправки, можно открыть отправителя.</span><span class="sxs-lookup"><span data-stu-id="ae524-138">To reuse the same connection for multiple send calls, you can open a sender:</span></span>
```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```
<span data-ttu-id="ae524-139">При использовании асинхронного клиента, в указанных выше операциях используется синтаксис async.</span><span class="sxs-lookup"><span data-stu-id="ae524-139">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
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


### <a name="receiving-messages"></a><span data-ttu-id="ae524-140">Получение сообщений</span><span class="sxs-lookup"><span data-stu-id="ae524-140">Receiving messages</span></span>
<span data-ttu-id="ae524-141">Сообщения можно получать из очереди в рамках цикла непрерывной итерации.</span><span class="sxs-lookup"><span data-stu-id="ae524-141">Messages can be received from a queue as a continuous iterator.</span></span> <span data-ttu-id="ae524-142">Режим по умолчанию для приема сообщений — [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read). Для включения этого режима требуется, чтобы каждое сообщение было явно завершено для его удаления из очереди.</span><span class="sxs-lookup"><span data-stu-id="ae524-142">The default mode for message receiving is [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), which requires each message to be explicitly completed in order that it be removed from the queue.</span></span>
```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```
<span data-ttu-id="ae524-143">Подключение службы будет оставаться открытым на протяжении всего цикла итерации.</span><span class="sxs-lookup"><span data-stu-id="ae524-143">The service connection will remain open for the entirety of the iterator.</span></span>
<span data-ttu-id="ae524-144">Если для потока сообщений выполняется только частичная итерация, запустите получатель в операторе `with`, чтобы закрыть подключение.</span><span class="sxs-lookup"><span data-stu-id="ae524-144">If you find yourself only partially iterating the message stream, you should run the receiver in a `with` statement to ensure the connection is closed:</span></span>
```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
<span data-ttu-id="ae524-145">При использовании асинхронного клиента, в указанных выше операциях используется синтаксис async.</span><span class="sxs-lookup"><span data-stu-id="ae524-145">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a><span data-ttu-id="ae524-146">Разделы и подписки служебной шины</span><span class="sxs-lookup"><span data-stu-id="ae524-146">Service Bus topics and subscriptions</span></span>

<span data-ttu-id="ae524-147">Наряду с очередями служебной шины разделы и подписки служебной шины представляют еще один уровень абстракции. Эти сущности обеспечивают разновидность взаимодействия "один ко многим" в рамках схемы публикации и подписки.</span><span class="sxs-lookup"><span data-stu-id="ae524-147">Service Bus topics and subscriptions are an abstraction on top of Service Bus queues that provide a one-to-many form of communication, in a publish/subscribe pattern.</span></span> <span data-ttu-id="ae524-148">Сообщения отправляются в раздел и доставляются в одну или несколько связанных подписок. Это особенно удобно при масштабировании с учетом большого количества получателей.</span><span class="sxs-lookup"><span data-stu-id="ae524-148">Messages are sent to a topic and delivered to one or more associated subscriptions, which is useful for scaling to large numbers of recipients.</span></span>

### <a name="create-topic"></a><span data-ttu-id="ae524-149">Создание раздела</span><span class="sxs-lookup"><span data-stu-id="ae524-149">Create topic</span></span>
<span data-ttu-id="ae524-150">Вы можете создать раздел в пространстве имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="ae524-150">This creates a new topic within the Service Bus namespace.</span></span> <span data-ttu-id="ae524-151">Если раздел с тем же именем уже существует, возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="ae524-151">If a topic of the same name already exists an error will be raised.</span></span> 
```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a><span data-ttu-id="ae524-152">Получение клиента раздела</span><span class="sxs-lookup"><span data-stu-id="ae524-152">Get a topic client</span></span>
<span data-ttu-id="ae524-153">TopicClient можно использовать для отправки сообщений в раздел, а также других операций.</span><span class="sxs-lookup"><span data-stu-id="ae524-153">A TopicClient can be used to send messages to the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a><span data-ttu-id="ae524-154">Создание подписки</span><span class="sxs-lookup"><span data-stu-id="ae524-154">Create subscription</span></span>
<span data-ttu-id="ae524-155">Вы можете создать подписку для указанного раздела в пространстве имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="ae524-155">This creates a new subscription for the specified topic within the Service Bus namespace.</span></span>
```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a><span data-ttu-id="ae524-156">Получение клиента подписки</span><span class="sxs-lookup"><span data-stu-id="ae524-156">Get a subscription client</span></span>
<span data-ttu-id="ae524-157">SubscriptionClient можно использовать для получения сообщений из раздела, а также других операций.</span><span class="sxs-lookup"><span data-stu-id="ae524-157">A SubscriptionClient can be used to receive messages from the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a><span data-ttu-id="ae524-158">Переход с версии 0.21.1 на версию 0.50.0</span><span class="sxs-lookup"><span data-stu-id="ae524-158">Migration from v0.21.1 to v0.50.0</span></span>
<span data-ttu-id="ae524-159">В версии 0.50.0 представлены основные критические изменения.</span><span class="sxs-lookup"><span data-stu-id="ae524-159">Major breaking changes were introduced in version 0.50.0.</span></span>
<span data-ttu-id="ae524-160">Исходный API на основе HTTP по-прежнему доступен в версии 0.50.0, но теперь он включен в новое пространство имен: `azure.servicebus.control_client`.</span><span class="sxs-lookup"><span data-stu-id="ae524-160">The original HTTP-based API is still available in v0.50.0 - however it now exists under a new namesapce: `azure.servicebus.control_client`.</span></span>

### <a name="should-i-upgrade"></a><span data-ttu-id="ae524-161">Следует ли выполнять обновление?</span><span class="sxs-lookup"><span data-stu-id="ae524-161">Should I upgrade?</span></span>
<span data-ttu-id="ae524-162">Новый пакет (версии 0.50.0) не включает улучшения операций на основе HTTP в сравнении с версией 0.21.1.</span><span class="sxs-lookup"><span data-stu-id="ae524-162">The new package (v0.50.0) offers no improvements in HTTP-based operations over v0.21.1.</span></span> <span data-ttu-id="ae524-163">API на основе HTTP является идентичным, за исключением того, что этот интерфейс включен в новое пространство имен.</span><span class="sxs-lookup"><span data-stu-id="ae524-163">The HTTP-based API is identical except that it now exists under a new namespace.</span></span> <span data-ttu-id="ae524-164">Поэтому, если вы хотите использовать операции на основе HTTP (`create_queue`, `delete_queue` и т.д.), сейчас вы не получите дополнительные преимущества от обновления.</span><span class="sxs-lookup"><span data-stu-id="ae524-164">For this reason if you only wish to use HTTP-based operations (`create_queue`, `delete_queue` etc) - there will be no additional benefit in upgrading at this time.</span></span>


### <a name="how-do-i-migrate-my-code-to-the-new-version"></a><span data-ttu-id="ae524-165">Как перенести код в новую версию?</span><span class="sxs-lookup"><span data-stu-id="ae524-165">How do I migrate my code to the new version?</span></span>
<span data-ttu-id="ae524-166">Код, написанный для версии 0.21.0, можно перенести в версию 0.50.0. Для этого нужно просто изменить пространство имен для импорта.</span><span class="sxs-lookup"><span data-stu-id="ae524-166">Code written against v0.21.0 can be ported to version 0.50.0 by simply changing the import namespace:</span></span>

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a><span data-ttu-id="ae524-167">Использование операций на основе HTTP в устаревшей версии API</span><span class="sxs-lookup"><span data-stu-id="ae524-167">Using HTTP-based operations of the legacy API</span></span>
<span data-ttu-id="ae524-168">В следующей документации описана устаревшая версия API. Она предназначена для тех, кто хочет перенести существующий код в версию 0.50.0 без внесения дополнительных изменений.</span><span class="sxs-lookup"><span data-stu-id="ae524-168">The following documentation describes the legacy API and should be used for those wishing to port existing code to v0.50.0 without making any additional changes.</span></span> <span data-ttu-id="ae524-169">Эти справочные материалы также можно использовать как рекомендации для пользователей версии 0.21.1.</span><span class="sxs-lookup"><span data-stu-id="ae524-169">This reference can also be used as guidance by those using v0.21.1.</span></span>
<span data-ttu-id="ae524-170">Для тех, кто создает новый код, мы рекомендуем использовать новый API, описанный выше.</span><span class="sxs-lookup"><span data-stu-id="ae524-170">For those writing new code, we recommend using the new API described above.</span></span>

### <a name="service-bus-queues"></a><span data-ttu-id="ae524-171">Очереди служебной шины</span><span class="sxs-lookup"><span data-stu-id="ae524-171">Service Bus queues</span></span>

#### <a name="shared-access-signature-sas-authentication"></a><span data-ttu-id="ae524-172">Аутентификация SAS</span><span class="sxs-lookup"><span data-stu-id="ae524-172">Shared Access Signature (SAS) authentication</span></span>

<span data-ttu-id="ae524-173">Чтобы использовать аутентификацию SAS, создайте служебную шину:</span><span class="sxs-lookup"><span data-stu-id="ae524-173">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a><span data-ttu-id="ae524-174">Аутентификация службы контроля доступа (ACS)</span><span class="sxs-lookup"><span data-stu-id="ae524-174">Access Control Service (ACS) authentication</span></span>
<span data-ttu-id="ae524-175">ACS не поддерживается в новом пространстве имен служебной шины.</span><span class="sxs-lookup"><span data-stu-id="ae524-175">ACS is no longer supported on new Service Bus namespaces.</span></span> <span data-ttu-id="ae524-176">Мы рекомендуем [перенести приложения для использования аутентификации SAS](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span><span class="sxs-lookup"><span data-stu-id="ae524-176">We recommend [migrating applications to SAS authentication](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span></span>
<span data-ttu-id="ae524-177">Чтобы использовать аутентификацию ACS в предыдущем пространстве имен служебной шины, создайте ServiceBusService:</span><span class="sxs-lookup"><span data-stu-id="ae524-177">To use ACS authentication within an older Service Bus namesapce, create the ServiceBusService with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
#### <a name="sending-and-receiving-messages"></a><span data-ttu-id="ae524-178">Отправка и получение сообщений</span><span class="sxs-lookup"><span data-stu-id="ae524-178">Sending and receiving messages</span></span>

<span data-ttu-id="ae524-179">Метод **create\_queue** можно использовать, чтобы проверить наличие очереди:</span><span class="sxs-lookup"><span data-stu-id="ae524-179">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="ae524-180">Затем можно вызвать метод **send\_queue\_message**, чтобы включить сообщение в очередь:</span><span class="sxs-lookup"><span data-stu-id="ae524-180">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="ae524-181">После этого можно вызвать метод **send\_queue\_message_batch**, чтобы одновременно отправить несколько сообщений:</span><span class="sxs-lookup"><span data-stu-id="ae524-181">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="ae524-182">Также можно вызвать метод **receive\_queue\_message**, чтобы исключить сообщение из очереди.</span><span class="sxs-lookup"><span data-stu-id="ae524-182">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a><span data-ttu-id="ae524-183">Разделы служебной шины</span><span class="sxs-lookup"><span data-stu-id="ae524-183">Service Bus topics</span></span>

<span data-ttu-id="ae524-184">Метод **create\_topic** можно использовать, чтобы создать раздел на стороне сервера:</span><span class="sxs-lookup"><span data-stu-id="ae524-184">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="ae524-185">Метод **send\_topic\_message** можно использовать, чтобы отправить сообщение в раздел:</span><span class="sxs-lookup"><span data-stu-id="ae524-185">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="ae524-186">Метод **send\_topic\_message** можно использовать, чтобы отправить несколько сообщений одновременно:</span><span class="sxs-lookup"><span data-stu-id="ae524-186">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="ae524-187">Учтите, что строковые сообщения в Python 3 отправляются в кодировке utf-8. В Python 2 кодировкой управляет пользователь.</span><span class="sxs-lookup"><span data-stu-id="ae524-187">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="ae524-188">Клиент затем может создать подписку и начать обрабатывать сообщения, вызывая методы **create\_subscription** и **receive\_subscription\_message**.</span><span class="sxs-lookup"><span data-stu-id="ae524-188">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="ae524-189">Обратите внимание на то, что все сообщения, отправленные до создания подписки, не будут получены.</span><span class="sxs-lookup"><span data-stu-id="ae524-189">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a><span data-ttu-id="ae524-190">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="ae524-190">Event Hub</span></span>

<span data-ttu-id="ae524-191">Центры событий собирают потоки событий с высокой пропускной способностью из разнородного набора устройств и служб.</span><span class="sxs-lookup"><span data-stu-id="ae524-191">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="ae524-192">Метод **create\_event\_hub** можно использовать, чтобы создать концентратор событий:</span><span class="sxs-lookup"><span data-stu-id="ae524-192">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="ae524-193">Отправка события</span><span class="sxs-lookup"><span data-stu-id="ae524-193">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="ae524-194">Содержимое событий — это сообщение о событии или строка в кодировке JSON, содержащая несколько сообщений.</span><span class="sxs-lookup"><span data-stu-id="ae524-194">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

### <a name="advanced-features"></a><span data-ttu-id="ae524-195">Дополнительные функции</span><span class="sxs-lookup"><span data-stu-id="ae524-195">Advanced features</span></span>

#### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="ae524-196">Свойства Broker и User</span><span class="sxs-lookup"><span data-stu-id="ae524-196">Broker properties and user properties</span></span>

<span data-ttu-id="ae524-197">В этом разделе описано, как использовать свойства Broker и User, определенные [здесь](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span><span class="sxs-lookup"><span data-stu-id="ae524-197">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```
<span data-ttu-id="ae524-198">Можно использовать значение даты и времени, целое число, число с плавающей запятой или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="ae524-198">You can use datetime, int, float or boolean</span></span>

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
<span data-ttu-id="ae524-199">Чтобы обеспечить совместимость со старой версией этой библиотеки, `broker_properties` также можно определить как строку JSON.</span><span class="sxs-lookup"><span data-stu-id="ae524-199">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="ae524-200">В такой ситуации создавать допустимую строку JSON должен пользователь. Средства Python не будут выполнять проверку до отправки в RestAPI.</span><span class="sxs-lookup"><span data-stu-id="ae524-200">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a><span data-ttu-id="ae524-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ae524-201">Next Steps</span></span>
* [<span data-ttu-id="ae524-202">Документация по служебной шине</span><span class="sxs-lookup"><span data-stu-id="ae524-202">Service Bus documentation</span></span>](https://docs.microsoft.com/azure/service-bus-messaging)
* [<span data-ttu-id="ae524-203">Исходный код пакета SDK</span><span class="sxs-lookup"><span data-stu-id="ae524-203">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="ae524-204">Справочная документация по пакету SDK</span><span class="sxs-lookup"><span data-stu-id="ae524-204">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [<span data-ttu-id="ae524-205">Дополнительные примеры</span><span class="sxs-lookup"><span data-stu-id="ae524-205">Additional samples</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
