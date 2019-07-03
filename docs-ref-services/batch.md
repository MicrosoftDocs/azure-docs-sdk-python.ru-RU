---
title: Библиотеки пакетной службы Azure для Python
description: Справочная документация по библиотекам пакетной службы для Python
keywords: Azure, Python, SDK, API, Batch, processing, scheduling, long-running
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: batch
ms.openlocfilehash: bbc691a8db6597c77575900b4e2a06f34ebb179c
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534357"
---
# <a name="azure-batch-libraries-for-python"></a>Библиотеки пакетной службы Azure для Python

## <a name="overview"></a>Обзор

Обеспечьте эффективную работу приложений для крупномасштабных параллельных и высокопроизводительных вычислений в облаке с помощью [пакетной службы Azure](/azure/batch/batch-technical-overview).

Чтобы приступить к работе с пакетной службой Azure, ознакомьтесь со статьей [Создание учетной записи пакетной службы на портале Azure](/azure/batch/batch-account-create-portal).

## <a name="install-the-libraries"></a>Установка библиотек

## <a name="client-library"></a>Клиентская библиотека
Клиентские библиотеки пакетной службы Azure позволяют настроить вычислительные узлы и пулы, определить и настроить выполняемые задачи в заданиях, а также настроить диспетчер заданий, чтобы отслеживать выполнение заданий и управлять им. Дополнительные сведения об использовании этих объектов для запуска решений для крупномасштабных параллельных вычислений см. [здесь](/azure/batch/batch-api-basics).

```bash
pip install azure-batch
```
### <a name="example"></a>Пример

Настройте пул вычислительных узлов Linux в учетной записи пакетной службы.

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

## <a name="management-api"></a>API управления
Используйте библиотеки управления пакетной службы Azure, чтобы создавать и удалять учетные записи пакетной службы, считывать и повторно создавать ключи учетной записи пакетной службы и управлять хранилищем учетных записей пакетной службы.

```bash
pip install azure-mgmt-batch
```
> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/python/api/overview/azure/batch/client)

### <a name="example"></a>Пример
Создайте учетную запись пакетной службы Azure и настройте новое приложение и учетную запись хранения Azure для него.

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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/batch/management)
