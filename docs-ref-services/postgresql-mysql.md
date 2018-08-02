---
title: Библиотеки Azure MySQL и PostgreSQL для Python
description: ''
keywords: Azure, Python, SDK, API, SQL, database, MySQL, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.openlocfilehash: e3cd84288ad8d49cfcd673506e2db150c02e7918
ms.sourcegitcommit: 16eecfc4ed0e2a8344ce5887327cdf2619ba89e4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/21/2018
ms.locfileid: "39189594"
---
# <a name="azure-mysqlpostgresql-libraries-for-python"></a>Библиотеки Azure MySQL и PostgreSQL для Python

## <a name="mysql"></a>MySQL

Для работы с ресурсами и данными, хранящимися в [базе данных Azure MySQL](/azure/mysql/overview), с помощью Python используйте диспетчер MySQL и модуль pyodbc.

### <a name="client-odbc-driver-and-pyodbc"></a>Драйвер клиента ODBC и модуль pyodbc

Рекомендуемой клиентской библиотекой для доступа к базе данных Azure для MySQL является [драйвер Microsoft ODBC](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries). Подключитесь к базе данных при помощи драйвера ODBC и напрямую выполните инструкции SQL.

#### <a name="example"></a>Пример

Подключитесь к базе данных Azure для MySQL и выберите все записи в таблице sales. Строку подключения ODBC для базы данных можно получить на портале Azure.

```python
SERVER = 'YOUR_SEVER_NAME' + '.mysql.database.azure.com'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_MYSQL_USERNAME'
PASSWORD = 'YOUR_MYSQL_PASSWORD'

DRIVER = '{MySQL ODBC 5.3 UNICODE Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=3306;SERVER=' + SERVER + ';PORT=3306;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

### <a name="management-api"></a>API управления

Создавайте ресурсы MySQL и управляйте ими в своей подписке с помощью API управления.

#### <a name="requirements"></a>Требования
Необходимо установить библиотеки управления MySQL для Python.
```bash
pip install azure-mgmt-rdbms
```

Дополнительные сведения о получении учетных данных для проверки подлинности с помощью клиента управления см. в разделе, посвященном [проверке подлинности с помощью пакета SDK для Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).

#### <a name="example"></a>Пример

Создайте ресурс базы данных MySQL 5.7 и ограничьте доступ к диапазону IP-адресов с помощью правила брандмауэра.

```python

from azure.mgmt.rdbms.mysql import MySQLManagementClient
from azure.mgmt.rdbms.mysql.models import ServerForCreate, ServerPropertiesForDefaultCreate, ServerVersion

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE-GROUP_WITH_POSTGRES"
MYSQL_SERVER = "YOUR_DESIRED_MYSQL_SERVER_NAME"
MYSQL_ADMIN_USER = "YOUR_MYSQL_ADMIN_USERNAME"
MYSQL_ADMIN_PASSWORD = "YOUR_MYSQL_ADMIN_PASSOWRD"
LOCATION = "westus"  # example Azure availability zone, should match resource group


client = MySQLManagementClient(credentials=creds,
    subscription_id=SUBSCRIPTION_ID)

server_creation_poller = client.servers.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=MYSQL_SERVER,
    ServerForCreate(
        ServerPropertiesForDefaultCreate(
            administrator_login=MYSQL_ADMIN_USER,
            administrator_login_password=MYSQL_ADMIN_PASSWORD,
            version=ServerVersion.five_full_stop_seven
        ),
        location=LOCATION
    )
)

server = server_creation_poller.result()

# Open access to this server for IPs
rule_creation_poller = client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    MYSQL_SERVER,
    "some_custom_ip_range_whitelist_rule_name",  # Custom firewall rule name
    "123.123.123.123",  # Start ip range
    "167.220.0.235"  # End ip range
)

firewall_rule = rule_creation_poller.result()
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/postgresql/mysql/management)

## <a name="postgresql"></a>PostgreSQL
Подключитесь к базе данных при помощи драйвера ODBC и модуля pyodbc и напрямую выполните инструкции SQL.

Дополнительные сведения о [базе данных Azure для PostgreSQL](https://docs.microsoft.com/azure/postgresql/).

### <a name="client-odbc-driver-and-pyodbc"></a>Драйвер клиента ODBC и модуль pyodbc
Рекомендуемой клиентской библиотекой для доступа к базе данных Azure для PostgreSQL являются [драйвер Microsoft ODBC и модуль pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).

#### <a name="example"></a>Пример 

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

### <a name="management-api"></a>API управления
#### <a name="requirements"></a>Требования
Необходимо установить библиотеки управления PostgreSQL для Python.
```bash
pip install azure-mgmt-rdbms
```

Дополнительные сведения о получении учетных данных для проверки подлинности с помощью клиента управления см. в разделе, посвященном [проверке подлинности с помощью пакета SDK для Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).

#### <a name="example"></a>Пример
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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/postgresql/mysql/management)