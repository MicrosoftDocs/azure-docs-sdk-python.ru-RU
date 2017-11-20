---
title: "Библиотеки Azure PostgreSQL для Python"
description: 
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
ms.openlocfilehash: e184efc276fb4e6d86504ab44e47340ce72e7006
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
#<a name="azure-postgresql-libraries-for-python"></a><span data-ttu-id="6f761-103">Библиотеки Azure PostgreSQL для Python</span><span class="sxs-lookup"><span data-stu-id="6f761-103">Azure PostgreSQL libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="6f761-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6f761-104">Overview</span></span>
<span data-ttu-id="6f761-105">Подключитесь к базе данных при помощи драйвера ODBC и модуля pyodbc и напрямую выполните инструкции SQL.</span><span class="sxs-lookup"><span data-stu-id="6f761-105">Use the ODBC driver and pyodbc to connect to the database and execute SQL statements directly.</span></span>

<span data-ttu-id="6f761-106">Дополнительные сведения о [базе данных Azure для PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="6f761-106">Learn more about [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="6f761-107">Драйвер клиента ODBC и модуль pyodbc</span><span class="sxs-lookup"><span data-stu-id="6f761-107">Client ODBC driver and pyodbc</span></span>
<span data-ttu-id="6f761-108">Рекомендуемой клиентской библиотекой для доступа к базе данных Azure для PostgreSQL являются [драйвер Microsoft ODBC и модуль pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="6f761-108">The recommended client library for accessing Azure Database for PostgreSQL is the Microsoft [ODBC driver and pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)</span></span>

### <a name="example"></a><span data-ttu-id="6f761-109">Пример</span><span class="sxs-lookup"><span data-stu-id="6f761-109">Example</span></span> 

<span data-ttu-id="6f761-110">Подключитесь к базе данных Azure для PostgreSQL и выберите все записи в таблице `SALES`.</span><span class="sxs-lookup"><span data-stu-id="6f761-110">Connect to a Azure Database for PostgreSQL and select all records in the `SALES` table.</span></span> <span data-ttu-id="6f761-111">Строку подключения ODBC для базы данных можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6f761-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="6f761-112">API управления</span><span class="sxs-lookup"><span data-stu-id="6f761-112">Management API</span></span>
### <a name="requirements"></a><span data-ttu-id="6f761-113">Требования</span><span class="sxs-lookup"><span data-stu-id="6f761-113">Requirements</span></span>
<span data-ttu-id="6f761-114">Необходимо установить библиотеки управления PostgreSQL для Python.</span><span class="sxs-lookup"><span data-stu-id="6f761-114">You must install the PostgreSQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="6f761-115">Дополнительные сведения о получении учетных данных для проверки подлинности с помощью клиента управления см. в разделе, посвященном [проверке подлинности с помощью пакета SDK для Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="6f761-115">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="6f761-116">Пример</span><span class="sxs-lookup"><span data-stu-id="6f761-116">Example</span></span>
<span data-ttu-id="6f761-117">В этом примере мы создадим новую базу данных Postgres на существующем сервере Postgres.</span><span class="sxs-lookup"><span data-stu-id="6f761-117">In this example we will create a new Postgres database on our existing Postgres server.</span></span>
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
> [<span data-ttu-id="6f761-118">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="6f761-118">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/managementlibrary)

