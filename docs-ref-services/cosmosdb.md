---
title: Библиотеки Azure Cosmos DB для Python
description: Справочная документация по клиентским библиотекам Azure Cosmos DB для Python
keywords: Azure, Python, SDK, API, SQL, database, PostGres, Cosmos DB, NoSQL
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: bb5e2af6a28d9543cce0c1e80fab1575b78f8cfa
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534316"
---
# <a name="azure-cosmos-db-libraries-for-python"></a><span data-ttu-id="78126-104">Библиотеки Azure Cosmos DB для Python</span><span class="sxs-lookup"><span data-stu-id="78126-104">Azure Cosmos DB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="78126-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="78126-105">Overview</span></span>

<span data-ttu-id="78126-106">Использование Azure Cosmos DB в приложениях Python для хранения и запроса документов JSON в хранилище данных NoSQL.</span><span class="sxs-lookup"><span data-stu-id="78126-106">Use Azure Cosmos DB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="78126-107">См. дополнительные сведения об [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="78126-107">Learn more about [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="78126-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="78126-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="78126-109">Библиотека управления</span><span class="sxs-lookup"><span data-stu-id="78126-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="78126-110">Пример</span><span class="sxs-lookup"><span data-stu-id="78126-110">Example</span></span>

<span data-ttu-id="78126-111">Поиск совпадающих документов в Azure Cosmos DB с помощью SQL-подобного интерфейса запросов:</span><span class="sxs-lookup"><span data-stu-id="78126-111">Find matching documents in Azure CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python Azure Cosmos DB client
client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
# Create a database
db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })

# Create collection options
options = {
    'offerEnableRUPerMinuteThroughput': True,
    'offerVersion': "V2",
    'offerThroughput': 400
}

# Create a collection
collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)

# Create some documents
document1 = client.CreateDocument(collection['_self'],
    { 
        'id': 'server1',
        'Web Site': 0,
        'Cloud Service': 0,
        'Virtual Machine': 0,
        'name': 'some' 
    })

# Query them in SQL
query = { 'query': 'SELECT * FROM server s' }    

options = {} 
options['enableCrossPartitionQuery'] = True
options['maxItemCount'] = 2

result_iterable = client.QueryDocuments(collection['_self'], query, options)
results = list(result_iterable)

print(results)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="78126-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="78126-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="78126-113">Примеры</span><span class="sxs-lookup"><span data-stu-id="78126-113">Samples</span></span>

* [<span data-ttu-id="78126-114">Разработка приложения Python для доступа к данным, хранящимся в учетной записи API SQL Azure Cosmos DB, и управления ими</span><span class="sxs-lookup"><span data-stu-id="78126-114">Develop a Python app to access and manage data stored in Azure Cosmos DB SQL API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [<span data-ttu-id="78126-115">Разработка приложения Python для доступа к данным, хранящимся в учетной записи API MongoDB Azure Cosmos DB, и управления ими</span><span class="sxs-lookup"><span data-stu-id="78126-115">Develop a Python app to access and manage data stored in Azure Cosmos DB MongoDB API account</span></span>](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [<span data-ttu-id="78126-116">Разработка приложения Python для доступа к данным, хранящимся в учетной записи API Gremlin Azure Cosmos DB, и управления ими</span><span class="sxs-lookup"><span data-stu-id="78126-116">Develop a Python app to access and manage data stored in Azure Cosmos DB Gremlin API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [<span data-ttu-id="78126-117">Разработка приложения Python для доступа к данным, хранящимся в учетной записи API Cassandra Azure Cosmos DB, и управления ими</span><span class="sxs-lookup"><span data-stu-id="78126-117">Develop a Python app to access and manage data stored in Azure Cosmos DB Cassandra API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [<span data-ttu-id="78126-118">Разработка приложения Python для доступа к данным, хранящимся в учетной записи API таблиц Azure Cosmos DB, и управления ими</span><span class="sxs-lookup"><span data-stu-id="78126-118">Develop a Python app to access and manage data stored in Azure Cosmos DB Table API account</span></span>](https://github.com/Azure-Samples/storage-python-getting-started.git)


