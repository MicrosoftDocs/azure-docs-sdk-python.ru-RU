---
title: Библиотеки Azure Cosmos DB для Python
description: Справочная документация по клиентским библиотекам Azure Cosmos DB для Python
keywords: Azure, Python, SDK, API, SQL, database, PostGres, Cosmos DB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: c2f3ea017a8864d4d2fb74a439c420f1f0313082
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276798"
---
# <a name="azure-cosmos-db-libraries-for-python"></a>Библиотеки Azure Cosmos DB для Python

## <a name="overview"></a>Обзор

Использование Azure Cosmos DB в приложениях Python для хранения и запроса документов JSON в хранилище данных NoSQL.

См. дополнительные сведения об [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

## <a name="client-library"></a>Клиентская библиотека
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>Библиотека управления
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>Пример

Поиск совпадающих документов в Azure Cosmos DB с помощью SQL-подобного интерфейса запросов:

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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a>Примеры

* [Разработка приложения Python для доступа к данным, хранящимся в учетной записи API SQL Azure Cosmos DB, и управления ими](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [Разработка приложения Python для доступа к данным, хранящимся в учетной записи API MongoDB Azure Cosmos DB, и управления ими](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [Разработка приложения Python для доступа к данным, хранящимся в учетной записи API Gremlin Azure Cosmos DB, и управления ими](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [Разработка приложения Python для доступа к данным, хранящимся в учетной записи API Cassandra Azure Cosmos DB, и управления ими](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [Разработка приложения Python для доступа к данным, хранящимся в учетной записи API таблиц Azure Cosmos DB, и управления ими](https://github.com/Azure-Samples/storage-python-getting-started.git)


