---
title: "Библиотеки Azure MySQL для Python"
description: 
keywords: Azure, Python, SDK, API, SQL, database, MySQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: mysql
ms.openlocfilehash: f03134bfddfabc426cbcaf4d98ef86d14038861f
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
---
# <a name="azure-mysql-libraries-for-python"></a><span data-ttu-id="4b8d5-103">Библиотеки Azure MySQL для Python</span><span class="sxs-lookup"><span data-stu-id="4b8d5-103">Azure MySQL libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="4b8d5-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4b8d5-104">Overview</span></span>

<span data-ttu-id="4b8d5-105">Для работы с ресурсами и данными, хранящимися в [базе данных Azure MySQL](/azure/mysql/overview), с помощью Python используйте диспетчер MySQL и модуль pyodbc.</span><span class="sxs-lookup"><span data-stu-id="4b8d5-105">Work with resources and data stored in [Azure MySQL Database](/azure/mysql/overview) from python with the MySQL manager and pyodbc.</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="4b8d5-106">Драйвер клиента ODBC и модуль pyodbc</span><span class="sxs-lookup"><span data-stu-id="4b8d5-106">Client ODBC driver and pyodbc</span></span>

<span data-ttu-id="4b8d5-107">Рекомендуемой клиентской библиотекой для доступа к базе данных Azure для MySQL является [драйвер Microsoft ODBC](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="4b8d5-107">The recommended client library for accessing Azure Database for MySQL is the Microsoft [ODBC driver](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span></span> <span data-ttu-id="4b8d5-108">Подключитесь к базе данных при помощи драйвера ODBC и напрямую выполните инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="4b8d5-108">Use the ODBC driver to connect to the database and execute SQL statements directly.</span></span>

### <a name="example"></a><span data-ttu-id="4b8d5-109">Пример</span><span class="sxs-lookup"><span data-stu-id="4b8d5-109">Example</span></span>

<span data-ttu-id="4b8d5-110">Подключитесь к базе данных Azure для MySQL и выберите все записи в таблице sales.</span><span class="sxs-lookup"><span data-stu-id="4b8d5-110">Connect to a Azure Database for MySQL and select all records in the sales table.</span></span> <span data-ttu-id="4b8d5-111">Строку подключения ODBC для базы данных можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4b8d5-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="4b8d5-112">API управления</span><span class="sxs-lookup"><span data-stu-id="4b8d5-112">Management API</span></span>

<span data-ttu-id="4b8d5-113">Создавайте ресурсы MySQL и управляйте ими в своей подписке с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="4b8d5-113">Create and manage MySQL resources in your subscription with the management API.</span></span>

### <a name="requirements"></a><span data-ttu-id="4b8d5-114">Требования</span><span class="sxs-lookup"><span data-stu-id="4b8d5-114">Requirements</span></span>
<span data-ttu-id="4b8d5-115">Необходимо установить библиотеки управления MySQL для Python.</span><span class="sxs-lookup"><span data-stu-id="4b8d5-115">You must install the MySQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="4b8d5-116">Дополнительные сведения о получении учетных данных для проверки подлинности с помощью клиента управления см. в разделе, посвященном [проверке подлинности с помощью пакета SDK для Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="4b8d5-116">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="4b8d5-117">Пример</span><span class="sxs-lookup"><span data-stu-id="4b8d5-117">Example</span></span>

<span data-ttu-id="4b8d5-118">Создайте ресурс базы данных MySQL 5.7 и ограничьте доступ к диапазону IP-адресов с помощью правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="4b8d5-118">Create a MySQL 5.7 Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

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
> [<span data-ttu-id="4b8d5-119">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="4b8d5-119">Explore the Management APIs</span></span>](/python/api/overview/azure/mysql/management)