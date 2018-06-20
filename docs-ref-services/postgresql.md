---
title: Библиотеки Azure PostgreSQL для Python
description: ''
keywords: Azure, Python, SDK, API, SQL, database, Postgres, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: postgresql
ms.openlocfilehash: cad5995072d5040764986765d9a900f46f5141ec
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478937"
---
#<a name="azure-postgresql-libraries-for-python"></a>Библиотеки Azure PostgreSQL для Python

## <a name="overview"></a>Обзор
Подключитесь к базе данных при помощи драйвера ODBC и модуля pyodbc и напрямую выполните инструкции SQL.

Дополнительные сведения о [базе данных Azure для PostgreSQL](https://docs.microsoft.com/azure/postgresql/).

## <a name="client-odbc-driver-and-pyodbc"></a>Драйвер клиента ODBC и модуль pyodbc
Рекомендуемой клиентской библиотекой для доступа к базе данных Azure для PostgreSQL являются [драйвер Microsoft ODBC и модуль pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).

### <a name="example"></a>Пример 

Подключитесь к базе данных Azure для PostgreSQL и выберите все записи в таблице `SALES`. Строку подключения ODBC для базы данных можно получить на портале Azure.

```python
import pyodbc

SERVER = 'YOUR_SERVER_NAME.postgres.database.azure.com'
DATABASE = 'YOUR_DB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

DRIVER = '{PostgreSQL ODBC Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=5432;SERVER=' + SERVER +
    ';PORT=5432;DATABASE=' + DATABASE + ';UID=' + USERNAME +
    ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES" # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a>API управления
### <a name="requirements"></a>Требования
Необходимо установить библиотеки управления PostgreSQL для Python.
```bash
pip install azure-mgmt-rdbms
```

Дополнительные сведения о получении учетных данных для проверки подлинности с помощью клиента управления см. в разделе, посвященном [проверке подлинности с помощью пакета SDK для Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).

### <a name="example"></a>Пример
В этом примере мы создадим новую базу данных Postgres на существующем сервере Postgres.
```python
from azure.mgtm.rdbms.postgresql import PostgreSQLManagementClient

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE_GROUP_WITH_POSTGRES"
POSTGRES_SERVER = "YOUR_POSTGRES_SERVER_NAME"
DB_NAME = "YOUR_DESIRED_DATABASE_NAME"

client = PostgreSQLManagementClient(credentials, SUBSCRIPTION_ID)

db_creation_poller = client.databases.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=POSTGRES_SERVER, database_name=DB_NAME)
db = db_creation_poller.result()
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/postgresql/management)

