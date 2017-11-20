---
title: "Библиотеки служебной шины для Python"
description: "Справочная документация по клиентским библиотекам и библиотекам управления служебной шины для Python"
keywords: Azure, Python, SDK, API, messaging, pubsub, pub-sub, message broker
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: bf7be945f2c7a3daea93ff4e5b770459c00632c8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="c8dc3-104">Библиотеки служебной шины для Python</span><span class="sxs-lookup"><span data-stu-id="c8dc3-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="c8dc3-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="c8dc3-105">Overview</span></span>

<span data-ttu-id="c8dc3-106">Служебная шина Microsoft Azure поддерживает набор облачных технологий промежуточного уровня, ориентированных на обработку сообщений. Эти технологии представлены надежными очередями сообщений, а также возможностями публикации и подписки в рамках обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="c8dc3-107">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="c8dc3-107">Install the libraries</span></span>
```bash
pip install azure-mgmt-servicebus
```

## <a name="example"></a><span data-ttu-id="c8dc3-108">Пример</span><span class="sxs-lookup"><span data-stu-id="c8dc3-108">Example</span></span>
<span data-ttu-id="c8dc3-109">Отправка сообщений в очередь.</span><span class="sxs-lookup"><span data-stu-id="c8dc3-109">Send messages to a queue.</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
# dequeue the message
msg = sbs.receive_queue_message('taskqueue')
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="c8dc3-110">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="c8dc3-110">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/managementlibrary)

