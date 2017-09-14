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
# <a name="azure-redis-cache-libraries-for-python"></a><span data-ttu-id="1e8d5-104">Библиотеки кэша Redis для Azure для Python</span><span class="sxs-lookup"><span data-stu-id="1e8d5-104">Azure Redis Cache libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="1e8d5-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="1e8d5-105">Overview</span></span>

<span data-ttu-id="1e8d5-106">Кэш Redis для Azure основан на популярном проекте с открытым кодом Redis.</span><span class="sxs-lookup"><span data-stu-id="1e8d5-106">Azure Redis Cache is based on the popular open source Redis project.</span></span> <span data-ttu-id="1e8d5-107">Он предоставляет доступ к безопасному выделенному экземпляру Redis, управляемому корпорацией Майкрософт и доступному из приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="1e8d5-107">It gives you access to a secure, dedicated Redis instance, managed by Microsoft and accessible from your Azure apps.</span></span>

<span data-ttu-id="1e8d5-108">Redis — это усовершенствованное хранилище пар "ключ — значение", где ключи могут содержать такие структуры данных, как строки, хэши, списки, наборы и сортируемые наборы.</span><span class="sxs-lookup"><span data-stu-id="1e8d5-108">Redis is an advanced key-value store, where keys can contain data structures such as strings, hashes, lists, sets, and sorted sets.</span></span> <span data-ttu-id="1e8d5-109">Redis поддерживает ряд атомарных операций с этими типами данных.</span><span class="sxs-lookup"><span data-stu-id="1e8d5-109">Redis supports a set of atomic operations on these data types.</span></span>

<span data-ttu-id="1e8d5-110">Дополнительные сведения о [кэше Redis для Azure](https://docs.microsoft.com/azure/redis-cache/).</span><span class="sxs-lookup"><span data-stu-id="1e8d5-110">Learn more about [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).</span></span>

## <a name="management-api"></a><span data-ttu-id="1e8d5-111">API управления</span><span class="sxs-lookup"><span data-stu-id="1e8d5-111">Management API</span></span>

<span data-ttu-id="1e8d5-112">Создавайте ресурсы Redis и управляйте ими в своей подписке с помощью API управления для Redis.</span><span class="sxs-lookup"><span data-stu-id="1e8d5-112">Create and manage your Redis resources in your subscription with the Redis management API.</span></span>

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a><span data-ttu-id="1e8d5-113">Пример</span><span class="sxs-lookup"><span data-stu-id="1e8d5-113">Example</span></span>

<span data-ttu-id="1e8d5-114">В приведенном ниже примере создается новый кэш Redis.</span><span class="sxs-lookup"><span data-stu-id="1e8d5-114">The following example creates a new Redis cache:</span></span>

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
> [<span data-ttu-id="1e8d5-115">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="1e8d5-115">Explore the Management APIs</span></span>](/python/api/overview/azure/redis/managementlibrary)

