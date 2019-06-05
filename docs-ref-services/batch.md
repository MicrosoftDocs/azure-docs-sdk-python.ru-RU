---
title: Библиотеки пакетной службы Azure для Python
description: Справочная документация по библиотекам пакетной службы для Python
keywords: Azure, Python, SDK, API, Batch, processing, scheduling, long-running
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: batch
ms.openlocfilehash: fb9528c449d197440590bfc3b1991065cfe13357
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376840"
---
# <a name="azure-batch-libraries-for-python"></a><span data-ttu-id="b474b-104">Библиотеки пакетной службы Azure для Python</span><span class="sxs-lookup"><span data-stu-id="b474b-104">Azure Batch libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="b474b-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="b474b-105">Overview</span></span>

<span data-ttu-id="b474b-106">Обеспечьте эффективную работу приложений для крупномасштабных параллельных и высокопроизводительных вычислений в облаке с помощью [пакетной службы Azure](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="b474b-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>

<span data-ttu-id="b474b-107">Чтобы приступить к работе с пакетной службой Azure, ознакомьтесь со статьей [Создание учетной записи пакетной службы на портале Azure](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="b474b-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="b474b-108">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="b474b-108">Install the libraries</span></span>

## <a name="client-library"></a><span data-ttu-id="b474b-109">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="b474b-109">Client library</span></span>
<span data-ttu-id="b474b-110">Клиентские библиотеки пакетной службы Azure позволяют настроить вычислительные узлы и пулы, определить и настроить выполняемые задачи в заданиях, а также настроить диспетчер заданий, чтобы отслеживать выполнение заданий и управлять им.</span><span class="sxs-lookup"><span data-stu-id="b474b-110">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="b474b-111">Дополнительные сведения об использовании этих объектов для запуска решений для крупномасштабных параллельных вычислений см. [здесь](/azure/batch/batch-api-basics).</span><span class="sxs-lookup"><span data-stu-id="b474b-111">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

```bash
pip install azure-batch
```
### <a name="example"></a><span data-ttu-id="b474b-112">Пример</span><span class="sxs-lookup"><span data-stu-id="b474b-112">Example</span></span>

<span data-ttu-id="b474b-113">Настройте пул вычислительных узлов Linux в учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b474b-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```python
# create the batch client for an account using its URI and keys
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

## <a name="management-api"></a><span data-ttu-id="b474b-114">API управления</span><span class="sxs-lookup"><span data-stu-id="b474b-114">Management API</span></span>
<span data-ttu-id="b474b-115">Используйте библиотеки управления пакетной службы Azure, чтобы создавать и удалять учетные записи пакетной службы, считывать и повторно создавать ключи учетной записи пакетной службы и управлять хранилищем учетных записей пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b474b-115">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

```bash
pip install azure-mgmt-batch
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="b474b-116">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="b474b-116">Explore the Client APIs</span></span>](/python/api/overview/azure/batch/client)

### <a name="example"></a><span data-ttu-id="b474b-117">Пример</span><span class="sxs-lookup"><span data-stu-id="b474b-117">Example</span></span>
<span data-ttu-id="b474b-118">Создайте учетную запись пакетной службы Azure и настройте новое приложение и учетную запись хранения Azure для него.</span><span class="sxs-lookup"><span data-stu-id="b474b-118">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```python
from azure.mgmt.batch import BatchManagementClient
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.storage import StorageManagementClient

LOCATION ='eastus'
GROUP_NAME ='batchresourcegroup'
STORAGE_ACCOUNT_NAME ='batchstorageaccount'

# Create Resource group
print('Create Resource Group')
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})

# Create a storage account
storage_async_operation = storage_client.storage_accounts.create(
    GROUP_NAME,
    STORAGE_ACCOUNT_NAME,
    StorageAccountCreateParameters(
        sku=Sku(SkuName.standard_ragrs),
        kind=Kind.storage,
        location=LOCATION
    )
)
storage_account = storage_async_operation.result()

# Create a Batch Account, specifying the storage account we want to link
storage_resource = storage_account.id
batch_account = azure.mgmt.batch.models.BatchAccountCreateParameters(
    location=LOCATION,
    auto_storage=azure.mgmt.batch.models.AutoStorageBaseProperties(storage_resource)
)
creating = batch_client.account.create('MyBatchAccount', LOCATION, batch_account)
creating.wait()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b474b-119">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="b474b-119">Explore the Management APIs</span></span>](/python/api/overview/azure/batch/management)
