---
title: "Начало работы с библиотеками Azure для Python"
description: "Начало работы с библиотеками Azure для Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: get-started
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 848ca9dc40000e68e5e3cea3af8b8a0d22747881
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-azure-libraries-for-python"></a><span data-ttu-id="e01e2-104">Начало работы с библиотеками Azure для Python</span><span class="sxs-lookup"><span data-stu-id="e01e2-104">Get started with the Azure libraries for Python</span></span>

<span data-ttu-id="e01e2-105">В этом руководстве объясняется, как использовать различные библиотеки Azure для Python.</span><span class="sxs-lookup"><span data-stu-id="e01e2-105">This guide demonstrates the usage of several Azure libraries for Python.</span></span>  <span data-ttu-id="e01e2-106">Вы настроите проверку подлинности, создадите и будете использовать учетную запись хранения Azure и базу данных SQL Azure, а также развернете несколько виртуальных машин и веб-приложение службы приложений Azure из GitHub.</span><span class="sxs-lookup"><span data-stu-id="e01e2-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e01e2-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e01e2-107">Prerequisites</span></span>

- <span data-ttu-id="e01e2-108">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e01e2-108">An Azure account.</span></span> <span data-ttu-id="e01e2-109">Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e01e2-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
- [<span data-ttu-id="e01e2-110">Python</span><span class="sxs-lookup"><span data-stu-id="e01e2-110">Python</span></span>](https://www.python.org/downloads/)
- <span data-ttu-id="e01e2-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) или [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e01e2-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

[!INCLUDE [azure-cloud-shell](../docs-ref-conceptual/includes/cloud-shell-try-it.md)]

## <a name="set-up-authentication"></a><span data-ttu-id="e01e2-112">Настройка проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="e01e2-112">Set up authentication</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e01e2-113">Эти инструкции следует применять в качестве краткого руководства по разработке.</span><span class="sxs-lookup"><span data-stu-id="e01e2-113">This should be used as quick start developer experience.</span></span> <span data-ttu-id="e01e2-114">В рабочей среде используйте [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) или свою систему учетных данных.</span><span class="sxs-lookup"><span data-stu-id="e01e2-114">For production purposes, use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) or your own credentials system.</span></span>
> <span data-ttu-id="e01e2-115">Любые изменения конфигурации CLI повлияют на выполнение пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="e01e2-115">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="e01e2-116">Пакет SDK позволяет создать клиент, используя активную подписку CLI.</span><span class="sxs-lookup"><span data-stu-id="e01e2-116">The SDK is able to create a client using your CLI active subscription.</span></span>

<span data-ttu-id="e01e2-117">Чтобы указать активные учетные данные, используйте команду [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e01e2-117">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="e01e2-118">По умолчанию используется существующий идентификатор подписки, но вы также можете указать его с помощью команды [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e01e2-118">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```
## <a name="create-a-virtual-environment"></a><span data-ttu-id="e01e2-119">Создание виртуальной среды</span><span class="sxs-lookup"><span data-stu-id="e01e2-119">Create a virtual environment</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e01e2-120">Создавать виртуальную среду не обязательно, но мы настоятельно рекомендуем сделать это.</span><span class="sxs-lookup"><span data-stu-id="e01e2-120">Create a virtual environment is optional, but we strongly suggest you to do it.</span></span>

<span data-ttu-id="e01e2-121">Создайте виртуальную среду в Bash ([Bash для Windows](https://msdn.microsoft.com/commandline/wsl/about) или Linux):</span><span class="sxs-lookup"><span data-stu-id="e01e2-121">Create a virtual environment in Bash (Linux or [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about)):</span></span>
```bash
pip install virtualenv
virtualenv mytestenv
cd mytestenv
source ./bin/activate
```

<span data-ttu-id="e01e2-122">Создайте виртуальную среду в PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e01e2-122">Create a virtual environment in Powershell:</span></span>
```powershell
pip install virtualenv
virtualenv mytestenv
cd mytestenv
.\Scripts\activate
```

> [!IMPORTANT]
> <span data-ttu-id="e01e2-123">Обратите внимание, что, если вы решили использовать [VSCode](https://code.visualstudio.com/) и [расширение для Python](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python), вы можете запустить его с помощью команды `code .` и настроить среду.</span><span class="sxs-lookup"><span data-stu-id="e01e2-123">Note that if you use [VSCode](https://code.visualstudio.com/) and the [Python extension](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python),  you can start it using `code .` and get your environment configured.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="e01e2-124">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="e01e2-124">Create a Linux virtual machine</span></span>
<span data-ttu-id="e01e2-125">Код в примере создает виртуальную машину Linux с именем `testLinuxVM` в группе ресурсов `sampleVmResourceGroup`, которая выполняется в регионе Azure "Восточная часть США".</span><span class="sxs-lookup"><span data-stu-id="e01e2-125">This code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleVmResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="e01e2-126">Выполните проверку подлинности:</span><span class="sxs-lookup"><span data-stu-id="e01e2-126">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e01e2-127">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e01e2-127">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus --n sampleVmResourceGroup
```

<span data-ttu-id="e01e2-128">Создайте виртуальную сеть и подсеть:</span><span class="sxs-lookup"><span data-stu-id="e01e2-128">Create a virtual network and subnet:</span></span>
```azurecli-interactive
az network vnet create -g sampleVmResourceGroup -n azure-sample-vnet --address-prefix 10.0.0.0/16 --subnet-name azure-sample-subnet --subnet-prefix 10.0.0.0/24
```

<span data-ttu-id="e01e2-129">Создайте общедоступный IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="e01e2-129">Create a public IP address:</span></span>
```azurecli-interactive
az network public-ip create -g sampleVmResourceGroup -n azure-sample-ip --allocation-method Dynamic --version IPv6
```
<span data-ttu-id="e01e2-130">Создайте клиент сетевого интерфейса:</span><span class="sxs-lookup"><span data-stu-id="e01e2-130">Create a network interface client:</span></span>
```azurecli-interactive
az network nic create -g sampleVmResourceGroup --vnet-name azure-sample-vnet --subnet azure-sample-subnet -n azure-sample-nic --public-ip-address azure-sample-ip
```

```python
from azure.mgmt.network import NetworkManagementClient
from azure.mgmt.compute import ComputeManagementClient
from azure.common.client_factory import get_client_from_cli_profile

# Azure Datacenter
LOCATION = 'eastus'

# Resource Group
GROUP_NAME = 'sampleVmResourceGroup'

# Network
VNET_NAME = 'azure-sample-vnet'
SUBNET_NAME = 'azure-sample-subnet'

# VM
NIC_NAME = 'azure-sample-nic'
VM_NAME = 'testLinuxVM'

USERNAME = 'userlogin'
PASSWORD = 'Pa$$w0rd91'

IP_ADDRESS_NAME='azure-sample-ip'

VM_REFERENCE = {
    'linux': {
        'publisher': 'Canonical',
        'offer': 'UbuntuServer',
        'sku': '16.04.0-LTS',
        'version': 'latest'
    },
    'windows': {
        'publisher': 'MicrosoftWindowsServerEssentials',
        'offer': 'WindowsServerEssentials',
        'sku': 'WindowsServerEssentials',
        'version': 'latest'
    }
}


def run_example():

    compute_client = get_client_from_cli_profile(ComputeManagementClient)
    network_client = get_client_from_cli_profile(NetworkManagementClient)

    # get nic id
    nic = network_client.network_interfaces.get(GROUP_NAME, NIC_NAME)

    # Create Linux VM
    print('\nCreating Linux Virtual Machine')
    vm_parameters = create_vm_parameters(nic.id, VM_REFERENCE['linux'])
    print(vm_parameters)
    async_vm_creation = compute_client.virtual_machines.create_or_update(
        GROUP_NAME, VM_NAME, vm_parameters)
    async_vm_creation.wait()


def create_vm_parameters(nic_id, vm_reference):
    """Create the VM parameters structure.
    """
    return {
        'location': LOCATION,
        'os_profile': {
            'computer_name': VM_NAME,
            'admin_username': USERNAME,
            'admin_password': PASSWORD
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': vm_reference['publisher'],
                'offer': vm_reference['offer'],
                'sku': vm_reference['sku'],
                'version': vm_reference['version']
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': nic_id,
            }]
        },
    }


if __name__ == "__main__":
    run_example()
```

<span data-ttu-id="e01e2-131">Когда программа завершит работу, проверьте виртуальную машину в подписке с помощью Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="e01e2-131">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="e01e2-132">Проверив, что код работает, используйте CLI, чтобы удалить виртуальную машину и ее ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e01e2-132">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="e01e2-133">Развертывание веб-приложения из репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="e01e2-133">Deploy a web app from a GitHub repo</span></span>
<span data-ttu-id="e01e2-134">Код в примере развертывает веб-приложение Flask из ветви `master` в репозитории GitHub в новое [веб-приложение службы приложений Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) уровня "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="e01e2-134">This code deploys a Flask web application from the `master` branch in a GitHub repo in to a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free tier.</span></span> 

<span data-ttu-id="e01e2-135">Сначала создайте вилку этого репозитория: https://github.com/Azure-Samples/python-docs-hello-world</span><span class="sxs-lookup"><span data-stu-id="e01e2-135">Before you begin: Fork https://github.com/Azure-Samples/python-docs-hello-world</span></span>

<span data-ttu-id="e01e2-136">Выполните проверку подлинности:</span><span class="sxs-lookup"><span data-stu-id="e01e2-136">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e01e2-137">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e01e2-137">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n sampleWebResourceGroup
```

<span data-ttu-id="e01e2-138">Создайте план службы приложений уровня "Бесплатный".</span><span class="sxs-lookup"><span data-stu-id="e01e2-138">Create a free app service plan:</span></span>
```azurecli-interactive
az appservice plan create -g sampleWebResourceGroup -n sampleFreePlan  --sku Free
```

```python
from azure.mgmt.web import WebSiteManagementClient
from azure.mgmt.web.models import Site, SiteSourceControl, SiteConfig
from azure.common.client_factory import get_client_from_cli_profile

RESOURCE_GROUP_NAME = 'sampleWebResourceGroup'
SERVICE_PLAN_NAME = 'sampleFreePlanName'
WEB_APP_NAME = 'sampleflaskapp123'
REPO_URL = 'GitHub_Repository_URL'

#log in
web_client = get_client_from_cli_profile(WebSiteManagementClient)

# get service plan id
service_plan = web_client.app_service_plans.get(RESOURCE_GROUP_NAME, SERVICE_PLAN_NAME)

# create a web app
siteConfiguration = SiteConfig(
    python_version='3.4',
)
site_async_operation = web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=service_plan.id,
        site_config=siteConfiguration
    ),
)

site = site_async_operation.result()
print('created webapp: ' + site.default_host_name)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url= REPO_URL,
        branch='master'
    )
)

source_control = source_control_async_operation.result()
print("added source control to: " + source_control.name + "azurewebsites.net")
```

<span data-ttu-id="e01e2-139">Откройте браузер и укажите приложение в CLI:</span><span class="sxs-lookup"><span data-stu-id="e01e2-139">Open a browser pointed to the application using the CLI:</span></span>
```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="e01e2-140">Проверив развертывание, удалите веб-приложение и план из подписки.</span><span class="sxs-lookup"><span data-stu-id="e01e2-140">Remove the web app and plan from your subscription once you've verified the deployment.</span></span> 
```azurecli-interactive
az group delete --name sampleWebResourceGroup
```


## <a name="connect-to-a-sql-database"></a><span data-ttu-id="e01e2-141">Подключение к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="e01e2-141">Connect to a SQL database</span></span>
<span data-ttu-id="e01e2-142">Код в примере создает базу данных SQL с правилом брандмауэра, разрешающим удаленный доступ, и подключается к ней с помощью драйвера Microsoft ODBC.</span><span class="sxs-lookup"><span data-stu-id="e01e2-142">This code creates a new SQL database with a firewall rule allowing remote access, and then connected to it using the Microsoft ODBC driver.</span></span> <span data-ttu-id="e01e2-143">Модуль pyodbc использует драйвер Microsoft ODBC в Linux для подключения к базам данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e01e2-143">Pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span></span> 

<span data-ttu-id="e01e2-144">Выполните проверку подлинности:</span><span class="sxs-lookup"><span data-stu-id="e01e2-144">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e01e2-145">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e01e2-145">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n azure-sample-group
```

<span data-ttu-id="e01e2-146">Создайте сервер SQL Server:</span><span class="sxs-lookup"><span data-stu-id="e01e2-146">Create a SQL server:</span></span>
```azurecli-interactive
az sql server create --admin-password HusH_Sec4et --admin-user mysecretname -l eastus -n samplesqlserver123 -g azure-sample-group
```

<span data-ttu-id="e01e2-147">Добавьте правило брандмауэра:</span><span class="sxs-lookup"><span data-stu-id="e01e2-147">Add firewall rule:</span></span>
```azurecli-interactive
az sql server firewall-rule create --end-ip-address 167.220.0.235 --name firewall_rule_name_123.123.123.123 --resource-group azure-sample-group --server samplesqlserver123 --start-ip-address 123.123.123.123
```

<span data-ttu-id="e01e2-148">Создайте базу данных SQL:</span><span class="sxs-lookup"><span data-stu-id="e01e2-148">Create a SQL database:</span></span>
```azurecli-interactive
az sql db create --name sample-db --resource-group azure-sample-group --server samplesqlserver123
```


```python
from azure.mgmt.sql import SqlManagementClient
from azure.common.client_factory import get_client_from_cli_profile
import pyodbc

LOCATION = 'eastus'
GROUP_NAME = 'azure-sample-group'
SERVER_NAME = 'samplesqlserver123'
DATABASE_NAME = 'sample-db'
USER_NAME ='mysecretname'
PASSWORD='HusH_Sec4et'

# authenticate
sql_client = get_client_from_cli_profile(SqlManagementClient)


def run_example():
    # Get SQL database
    print('Get SQL database')
    database = sql_client.databases.get(
        GROUP_NAME,
        SERVER_NAME,
        DATABASE_NAME
    )
    print(database)
    print("\n\n")


def create_and_insert():
    server = SERVER_NAME+'.database.windows.net'
    database = DATABASE_NAME
    username = USER_NAME
    password = PASSWORD
    driver = '{ODBC Driver 13 for SQL Server}'
    cnxn = pyodbc.connect(
        'DRIVER=' + driver + ';PORT=1433;SERVER=' + server + ';PORT=1443;DATABASE=' + database + ';UID=' + username + ';PWD=' + password)
    cursor = cnxn.cursor()
    tsql = "CREATE TABLE CLOUD (name varchar(255), code int);"
    tsqlInsert = "INSERT INTO CLOUD (name, code) VALUES ('Azure', 1); "
    selectValues = "SELECT * FROM CLOUD"
    with cursor.execute(tsql):
        print('Successfully created table!')
    with cursor.execute(tsqlInsert):
        print('Successfully inserted data into table')
    cursor.execute(selectValues)
    row = cursor.fetchone()
    while row:
        print(str(row[0]) + " " + str(row[1]))
        row = cursor.fetchone()
    cnxn.commit()

if __name__ == "__main__":
    run_example()
    create_and_insert()
```

<span data-ttu-id="e01e2-149">Убедившись, что код работает, удалите базу данных SQL и ее ресурсы с помощью CLI.</span><span class="sxs-lookup"><span data-stu-id="e01e2-149">Once you've verified that the code worked, use the CLI to delete the SQL database and its resources.</span></span>

```azurecli-interactive
az group delete --name azure-sample-group
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="e01e2-150">Запись большого двоичного объекта в новую учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="e01e2-150">Write a blob into a new storage account</span></span>

<span data-ttu-id="e01e2-151">Выполните проверку подлинности:</span><span class="sxs-lookup"><span data-stu-id="e01e2-151">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e01e2-152">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e01e2-152">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n sampleStorageResourceGroup
```

<span data-ttu-id="e01e2-153">Создайте учетную запись хранения:</span><span class="sxs-lookup"><span data-stu-id="e01e2-153">Create a storage account:</span></span>
```azurecli-interactive
az storage account create -n samplestorageaccountname -g sampleStorageResourceGroup -l eastus --sku Standard_RAGRS
```

<span data-ttu-id="e01e2-154">Этот код создает [учетную запись хранения Azure](https://docs.microsoft.com/azure/storage/storage-introduction), а затем использует библиотеки службы хранилища Azure для Python, чтобы создать HTML-файл в облаке.</span><span class="sxs-lookup"><span data-stu-id="e01e2-154">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Python to create a new html file in the cloud.</span></span> 
```python
from azure.storage import CloudStorageAccount
from azure.storage.blob import PublicAccess
from azure.storage.blob.models import ContentSettings
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.storage import StorageManagementClient

RESOURCE_GROUP = 'sampleStorageResourceGroup'
STORAGE_ACCOUNT_NAME = 'samplestorageaccountname'
CONTAINER_NAME = 'samplecontainername'

# log in
storage_client = get_client_from_cli_profile(StorageManagementClient)

# create a public storage container to hold the file
storage_keys = storage_client.storage_accounts.list_keys(RESOURCE_GROUP, STORAGE_ACCOUNT_NAME)
storage_keys = {v.key_name: v.value for v in storage_keys.keys}

storage_client = CloudStorageAccount(STORAGE_ACCOUNT_NAME, storage_keys['key1'])
blob_service = storage_client.create_block_blob_service()

blob_service.create_container(CONTAINER_NAME, public_access=PublicAccess.Container)

blob_service.create_blob_from_bytes(
    CONTAINER_NAME,
    'helloworld.html',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url(CONTAINER_NAME, 'helloworld.html'))
```
<span data-ttu-id="e01e2-155">Чтобы проверить, успешно ли отправлено содержимое, перейдите по выведенному URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="e01e2-155">To verify content successfully uploaded, navigate to the url printed.</span></span> 

<span data-ttu-id="e01e2-156">Удалите учетную запись хранилища с помощью CLI:</span><span class="sxs-lookup"><span data-stu-id="e01e2-156">Clean up the storage account using the CLI:</span></span>
```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="e01e2-157">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="e01e2-157">Explore more samples</span></span>

<span data-ttu-id="e01e2-158">Дополнительные сведения о том, как использовать библиотеки управления Azure для Python, чтобы управлять ресурсами и автоматизировать задачи, см. в наших примерах кода для [виртуальных машин](python-sdk-azure-web-apps-samples.md), [веб-приложений](python-sdk-azure-web-apps-samples.md) и [базы данных SQL](python-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e01e2-158">To learn more about how to use the Azure management libraries for Python to manage resources and automate tasks, see our sample code for [virtual machines](python-sdk-azure-web-apps-samples.md), [web apps](python-sdk-azure-web-apps-samples.md) and [SQL database](python-sdk-azure-sql-database-samples.md).</span></span>


## <a name="reference"></a><span data-ttu-id="e01e2-159">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="e01e2-159">Reference</span></span>

<span data-ttu-id="e01e2-160">[Справочник](/python/api/overview/azure/?view=azure-python) по всем пакетам.</span><span class="sxs-lookup"><span data-stu-id="e01e2-160">A [reference](/python/api/overview/azure/?view=azure-python) is available for all packages.</span></span>
