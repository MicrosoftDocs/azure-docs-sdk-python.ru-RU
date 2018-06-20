---
title: Библиотеки Azure Redis для Python
description: Справочная документация по клиентским библиотекам Redis для Python
keywords: Azure, Python, Redis, API, SDK, database, NoSQL
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: redis
ms.openlocfilehash: c2f8ebcbcbd7b71c1fa96e46a8148a3c0b88877f
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479247"
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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/redis/management)

