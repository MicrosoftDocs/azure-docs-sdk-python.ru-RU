---
title: Библиотеки базы данных SQL Azure для Python
description: Подключайтесь к базе данных SQL Azure с помощью драйвера ODBC и модуля pyodbc или управляйте экземплярами SQL Azure помощью API управления.
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 01/09/2018
ms.topic: reference
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: 5b73977fb58ed3cb17d675784da921b0e199d165
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2018
---
# <a name="azure-sql-database-libraries-for-python"></a>Библиотеки базы данных SQL Azure для Python

## <a name="overview"></a>Обзор

Работайте с данными, хранящимися в [базе данных SQL Azure](/azure/sql-database/sql-database-technical-overview), в коде Python с помощью модуля pyodbc и [драйвера базы данных ODBC](https://github.com/mkleehammer/pyodbc/wiki/Drivers-and-Driver-Managers). Просмотрите наше [краткое руководство](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) по подключению к базе данных SQL Azure и использованию инструкций Transact-SQL для запрашивания данных, а также [пример](https://github.com/mkleehammer/pyodbc/wiki/Getting-started) начала работы с pyodbc.

## <a name="install-odbc-driver-and-pyodbc"></a>Установка драйвера клиента ODBC и модуля pyodbc

```bash
pip install pyodbc
```
[Дополнительные сведения](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) об установке библиотек Python и библиотек обмена данными в базе данных.

## <a name="connect-and-execute-a-sql-query"></a>Подключение и выполнение SQL-запроса

### <a name="connect-to-a-sql-database"></a>Подключение к базе данных SQL

```python
import pyodbc

server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'

cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
```

### <a name="execute-a-sql-query"></a>Выполнение SQL-запроса

```python
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

> [!div class="nextstepaction"]
> [Пример pyodbc](https://github.com/mkleehammer/pyodbc/wiki/Getting-started)

## <a name="connecting-to-orms"></a>Подключение к моделям ORM

pyodbc работает и с другими моделями ORM, такими как [SQLAlchemy](http://docs.sqlalchemy.org/en/latest/dialects/mssql.html?highlight=pyodbc#module-sqlalchemy.dialects.mssql.pyodbc) и [Django](https://github.com/lionheart/django-pyodbc/). 

## <a name="management-apipythonapioverviewazuresqlmanagement"></a>[API управления](/python/api/overview/azure/sql/management)

Создавайте ресурсы базы данных SQL Azure и управляйте ими в своей подписке с помощью API управления. 

```bash
pip install azure-common
pip install azure-mgmt-sql
pip install azure-mgmt-resource
```

## <a name="example"></a>Пример

Создайте ресурс базы данных SQL и ограничьте доступ к диапазону IP-адресов с помощью правила брандмауэра.

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.sql import SqlManagementClient

RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_SERVER = 'yourvirtualsqlserver'
SQL_DB = 'YOUR_SQLDB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

# create resource client
resource_client = get_client_from_cli_profile(ResourceManagementClient)
# create resource group
resource_client.resource_groups.create_or_update(RESOURCE_GROUP, {'location': LOCATION})

sql_client = get_client_from_cli_profile(SqlManagementClient)

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_SERVER,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Create a SQL database in the Basic tier
database = sql_client.databases.create_or_update(
    RESOURCE_GROUP,
    SQL_SERVER,
    SQL_DB,
    {
        'location': LOCATION,
        'collation': 'SQL_Latin1_General_CP1_CI_AS',
        'create_mode': 'default',
        'requested_service_objective_name': 'Basic'
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/sql/management)

