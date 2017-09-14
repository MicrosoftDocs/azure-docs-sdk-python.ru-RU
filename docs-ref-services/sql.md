---
title: "Библиотеки базы данных SQL Azure для Python"
description: 
keywords: Azure, Python, SDK, API, SQL, database, pyodbc
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: b580c5011412bc77fd8fd55b709a305be07e2316
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-sql-database-libraries-for-python"></a>Библиотеки базы данных SQL Azure для Python

## <a name="overview"></a>Обзор

Работа с данными, хранящимися в [базе данных SQL Azure](/azure/sql-database/sql-database-technical-overview), в коде Python с помощью драйвера Microsoft ODBC и модуля pyodbc. 

## <a name="client-odbc-driver-and-pyodbc"></a>Драйвер клиента ODBC и модуль pyodbc

```bash
pip install pyodbc
```
Дополнительные сведения об установке Python и библиотек обмена данными в базе данных см. [здесь](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).

### <a name="example"></a>Пример

Подключение к базе данных SQL и выбор всех записей в таблице.

```python
import pyodbc 

SERVER = 'YOUR_SERVER_NAME.database.windows.net'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_DB_USERNAME'
PASSWORD = 'YOUR_DB_PASSWORD'

DRIVER= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER=' + DRIVER + ';PORT=1433;SERVER=' + SERVER +
    ';PORT=1443;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a>API управления

Создавайте ресурсы базы данных SQL Azure и управляйте ими в своей подписке с помощью API управления. 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a>Пример

Создайте ресурс базы данных SQL и ограничьте доступ к диапазону IP-адресов с помощью правила брандмауэра.

```python
RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_DB = 'YOUR_SQLDB_NAME'

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a>Примеры

* [Создание и администрирование баз данных SQL][1]    
* [Использование Python для подключения и создания запросов данных][2]   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) примеров кода для базы данных SQL Azure. 