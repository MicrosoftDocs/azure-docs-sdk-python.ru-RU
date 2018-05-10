---
title: Управляемые диски
description: Создание, изменение размера и обновление управляемого диска.
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: 733bd0ffce6ddb10219dae40bad6ea54e1efcd70
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2018
---
# <a name="managed-disks"></a>Управляемые диски

Теперь служба "Управляемые диски Azure" и 1000 виртуальных машин в масштабируемом наборе [доступны всем](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/). Служба "Управляемые диски Azure" обеспечивает простое управление дисками, расширенную масштабируемость и повышенную безопасность. Теперь вы можете забыть об учетных записях хранения для дисков и выполнять масштабирование, не беспокоясь об ограничениях, связанных с этими учетными записями. В этой публикации содержатся краткие вводные сведения и справочные материалы по использованию этой службы с помощью Python.



С точки зрения разработчика использование службы "Управляемые диски" с Azure CLI ничем не отличается от использования CLI в других кроссплатформенных средствах. Для администрирования управляемых дисков вы можете использовать пакеты Azure SDK для [Python](https://azure.microsoft.com/develop/python/) и [azure-mgmt-compute 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute). Вы также можете создать вычислительный клиент, следуя инструкциям из [этого руководства](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).


## <a name="standalone-managed-disks"></a>Автономные управляемые диски

Вы можете легко создавать автономные управляемые диски несколькими способами.

### <a name="create-an-empty-managed-disk"></a>Создание пустого управляемого диска.
```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'disk_size_gb': 20,
        'creation_data': {
            'create_option': DiskCreateOption.empty
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-blob-storage"></a>Создайте управляемый диск из хранилища BLOB-объектов.
```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.import_enum,
            'source_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd'
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-your-own-image"></a>Создание управляемого диска из своего образа
```python
from azure.mgmt.compute.models import DiskCreateOption

# If you don't know the id, do a 'get' like this to obtain it
managed_disk = compute_client.disks.get(self.group_name, 'myImageDisk')
async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.copy,
            'source_resource_id': managed_disk.id
        }
    }
)

disk_resource = async_creation.result()
```

## <a name="virtual-machine-with-managed-disks"></a>Виртуальная машина с управляемыми дисками

Вы можете создать виртуальную машину с неявным управляемым диском на основе определенного образа диска. Неявное создание управляемых дисков позволяет легко создавать диски, не указывая все сведения о них. Вам не нужно беспокоиться о создании учетных записей хранения и управлении ими.

Управляемый диск создается неявно при создании виртуальной машины в Azure из образа ОС. Теперь для параметра ``storage_profile`` не обязательно указывать ``os_disk``, и создание учетной записи хранения не является обязательным требованием для создания виртуальной машины.

```python
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        publisher='Canonical',
        offer='UbuntuServer',
        sku='16.04-LTS',
        version='latest'
    )
)
``` 
Указанный выше параметр ``storage_profile`` теперь считается допустимым. Полный пример создания виртуальной машины на Python (включая сеть и т. п.) см. в полном [руководстве по виртуальным машинам на Python](https://github.com/Azure-Samples/virtual-machines-python-manage).

Вы можете легко подключить ранее подготовленный управляемый диск.
```python
vm = compute.virtual_machines.get(
    'my_resource_group',
    'my_vm'
)
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
vm.storage_profile.data_disks.append({
    'lun': 12, # You choose the value, depending of what is available for you
    'name': managed_disk.name,
    'create_option': DiskCreateOptionTypes.attach,
    'managed_disk': {
        'id': managed_disk.id
    }
})
async_update = compute_client.virtual_machines.create_or_update(
    'my_resource_group',
    vm.name,
    vm,
)
async_update.wait()
```

## <a name="virtual-machine-scale-sets-with-managed-disks"></a>Масштабируемые наборы виртуальных машин с управляемыми дисками.

До выпуска службы "Управляемые диски" вам нужно было вручную создавать учетную запись хранения для всех необходимых виртуальных машин в масштабируемом наборе, а затем в REST API этого набора указывать параметр списка ``vhd_containers``, чтобы предоставить всем виртуальным машинам имя учетной записи хранения. Официальное руководство по переходу содержится в этой статье: `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.

Теперь благодаря управляемым дискам вы больше не будете иметь дела с учетными записями хранения. Если вы часто используете пакет SDK для масштабируемого набора виртуальных машин для Python, можно использовать такое же значение параметра ``storage_profile``, как и при создании виртуальной машины.

```python
'storage_profile': {
    'image_reference': {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "16.04-LTS",
        "version": "latest"
    }
},
```

Полный пример кода:

```python
naming_infix = "PyTestInfix"
vmss_parameters = {
    'location': self.region,
    "overprovision": True,
    "upgrade_policy": {
        "mode": "Manual"
    },
    'sku': {
        'name': 'Standard_A1',
        'tier': 'Standard',
        'capacity': 5
    },
    'virtual_machine_profile': {
        'storage_profile': {
            'image_reference': {
                "publisher": "Canonical",
                "offer": "UbuntuServer",
                "sku": "16.04-LTS",
                "version": "latest"
            }
        },
        'os_profile': {
            'computer_name_prefix': naming_infix,
            'admin_username': 'Foo12',
            'admin_password': 'BaR@123!!!!',
        },
        'network_profile': {
            'network_interface_configurations' : [{
                'name': naming_infix + 'nic',
                "primary": True,
                'ip_configurations': [{
                    'name': naming_infix + 'ipconfig',
                    'subnet': {
                        'id': subnet.id
                    } 
                }]
            }]
        }
    }
}

# Create VMSS test
result_create = compute_client.virtual_machine_scale_sets.create_or_update(
    'my_resource_group',
    'my_scale_set',
    vmss_parameters,
)
vmss_result = result_create.result()
``` 

## <a name="other-operations-with-managed-disks"></a>Другие операции с управляемыми дисками

### <a name="resizing-a-managed-disk"></a>Изменение размера управляемого диска

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.disk_size_gb = 25
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="update-the-storage-account-type-of-the-managed-disks"></a>Обновление типа учетной записи хранения управляемых дисков
```python
from azure.mgmt.compute.models import StorageAccountTypes

managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.account_type = StorageAccountTypes.standard_lrs
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="create-an-image-from-blob-storage"></a>Создание образа из хранилища BLOB-объектов
```python
async_create_image = compute_client.images.create_or_update(
    'my_resource_group',
    'myImage',
    {
        'location': 'westus',
        'storage_profile': {
            'os_disk': {
                'os_type': 'Linux',
                'os_state': "Generalized",
                'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
                'caching': "ReadWrite",
            }
        }
    }
)
image = async_create_image.result()
```

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a>Создание моментального снимка управляемого диска, который сейчас подключен к виртуальной машине
```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
async_snapshot_creation = self.compute_client.snapshots.create_or_update(
        'my_resource_group',
        'mySnapshot',
        {
            'location': 'westus',
            'creation_data': {
                'create_option': 'Copy',
                'source_uri': managed_disk.id
            }
        }
    )
snapshot = async_snapshot_creation.result()
```
