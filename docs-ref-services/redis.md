---
title: "Библиотеки Azure Redis для Python"
description: "Справочная документация по клиентским библиотекам Redis для Python"
keywords: Azure, Python, Redis, API, SDK, database, NoSQL
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: redis
ms.openlocfilehash: 3ba8d972e91fad229c1489800edeca08760254e6
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-redis-cache-libraries-for-python"></a>Библиотеки кэша Redis для Azure для Python

## <a name="overview"></a>Обзор

Кэш Redis для Azure основан на популярном проекте с открытым кодом Redis. Он предоставляет доступ к безопасному выделенному экземпляру Redis, управляемому корпорацией Майкрософт и доступному из приложений Azure.

Redis — это усовершенствованное хранилище пар "ключ — значение", где ключи могут содержать такие структуры данных, как строки, хэши, списки, наборы и сортируемые наборы. Redis поддерживает ряд атомарных операций с этими типами данных.

Дополнительные сведения о [кэше Redis для Azure](https://docs.microsoft.com/azure/redis-cache/).

## <a name="management-api"></a>API управления

Создавайте ресурсы Redis и управляйте ими в своей подписке с помощью API управления для Redis.

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a>Пример

В приведенном ниже примере создается новый кэш Redis.

```python
from azure.mgmt.redis import RedisManagementClient
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

redis_client = RedisManagementClient(
    credentials,
    subscription_id
)
group_name = 'myresourcegroup'
cache_name = 'mycachename'
redis_cache = redis_client.redis.create_or_update(
    group_name,
    cache_name,
    RedisCreateOrUpdateParameters(
        sku = Sku(name = 'Basic', family = 'C', capacity = '1'),
        location = "East US"
    )
)
# redis_cache is a RedisResourceWithAccessKey instance
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/redis/managementlibrary)

