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
# <a name="azure-sql-database-libraries-for-python"></a><span data-ttu-id="4c3b3-103">Библиотеки базы данных SQL Azure для Python</span><span class="sxs-lookup"><span data-stu-id="4c3b3-103">Azure SQL Database libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="4c3b3-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4c3b3-104">Overview</span></span>

<span data-ttu-id="4c3b3-105">Работа с данными, хранящимися в [базе данных SQL Azure](/azure/sql-database/sql-database-technical-overview), в коде Python с помощью драйвера Microsoft ODBC и модуля pyodbc.</span><span class="sxs-lookup"><span data-stu-id="4c3b3-105">Work with data stored in [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) from Python with the Microsoft ODBC driver and pyodbc.</span></span> 

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="4c3b3-106">Драйвер клиента ODBC и модуль pyodbc</span><span class="sxs-lookup"><span data-stu-id="4c3b3-106">Client ODBC driver and pyodbc</span></span>

```bash
pip install pyodbc
```
<span data-ttu-id="4c3b3-107">Дополнительные сведения об установке Python и библиотек обмена данными в базе данных см. [здесь](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="4c3b3-107">More details about installing the python and database communication libraries can be found [here](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span></span>

### <a name="example"></a><span data-ttu-id="4c3b3-108">Пример</span><span class="sxs-lookup"><span data-stu-id="4c3b3-108">Example</span></span>

<span data-ttu-id="4c3b3-109">Подключение к базе данных SQL и выбор всех записей в таблице.</span><span class="sxs-lookup"><span data-stu-id="4c3b3-109">Connect to a SQL database and select all records in a table.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="4c3b3-110">API управления</span><span class="sxs-lookup"><span data-stu-id="4c3b3-110">Management API</span></span>

<span data-ttu-id="4c3b3-111">Создавайте ресурсы базы данных SQL Azure и управляйте ими в своей подписке с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="4c3b3-111">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span> 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a><span data-ttu-id="4c3b3-112">Пример</span><span class="sxs-lookup"><span data-stu-id="4c3b3-112">Example</span></span>

<span data-ttu-id="4c3b3-113">Создайте ресурс базы данных SQL и ограничьте доступ к диапазону IP-адресов с помощью правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="4c3b3-113">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

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
> [<span data-ttu-id="4c3b3-114">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="4c3b3-114">Explore the Management APIs</span></span>](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a><span data-ttu-id="4c3b3-115">Примеры</span><span class="sxs-lookup"><span data-stu-id="4c3b3-115">Samples</span></span>

* <span data-ttu-id="4c3b3-116">[Создание и администрирование баз данных SQL][1]</span><span class="sxs-lookup"><span data-stu-id="4c3b3-116">[Create and manage SQL databases][1]</span></span>    
* <span data-ttu-id="4c3b3-117">[Использование Python для подключения и создания запросов данных][2]</span><span class="sxs-lookup"><span data-stu-id="4c3b3-117">[Use Python to connect and query data][2]</span></span>   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

<span data-ttu-id="4c3b3-118">Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) примеров кода для базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4c3b3-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) of Azure SQL database samples.</span></span> 