---
title: "Управляемые диски"
description: "Создание, изменение размера и обновление управляемого диска."
author: lisawong19
manager: douge
ms.assetid: 
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: 4154367f0449b174790ee3f3c9480ca0bceeea87
ms.sourcegitcommit: c6d9500492131bf782488fcafc7c5c41c2703e92
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/13/2017
---
# <a name="managed-disks"></a><span data-ttu-id="2be5c-103">Управляемые диски</span><span class="sxs-lookup"><span data-stu-id="2be5c-103">Managed Disks</span></span>

<span data-ttu-id="2be5c-104">Теперь служба "Управляемые диски Azure" и 1000 виртуальных машин в масштабируемом наборе [доступны всем](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/). Служба "Управляемые диски Azure" обеспечивает простое управление дисками, расширенную масштабируемость и повышенную безопасность.</span><span class="sxs-lookup"><span data-stu-id="2be5c-104">Azure Managed Disks and 1000 VMs in a Scale Set are now [generally available](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/) Azure Managed Disks provide a simplified disk Management, enhanced Scalability, better Security and Scale.</span></span> <span data-ttu-id="2be5c-105">Теперь вы можете забыть об учетных записях хранения для дисков и выполнять масштабирование, не беспокоясь об ограничениях, связанных с этими учетными записями.</span><span class="sxs-lookup"><span data-stu-id="2be5c-105">It takes away the notion of storage account for disks, enabling customers to scale without worrying about the limitations associated with storage accounts.</span></span> <span data-ttu-id="2be5c-106">В этой публикации содержатся краткие вводные сведения и справочные материалы по использованию этой службы с помощью Python.</span><span class="sxs-lookup"><span data-stu-id="2be5c-106">This post provides a quick introduction and reference on consuming the service from Python.</span></span>



<span data-ttu-id="2be5c-107">С точки зрения разработчика использование службы "Управляемые диски" с Azure CLI ничем не отличается от использования CLI в других кроссплатформенных средствах.</span><span class="sxs-lookup"><span data-stu-id="2be5c-107">From a developer perspective, the Managed Disks experience in Azure CLI is idomatic to the CLI experience in other cross-platform tools.</span></span> <span data-ttu-id="2be5c-108">Для администрирования управляемых дисков вы можете использовать пакеты Azure SDK для [Python](https://azure.microsoft.com/develop/python/) и [azure-mgmt-compute 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute).</span><span class="sxs-lookup"><span data-stu-id="2be5c-108">You can use the [Azure Python](https://azure.microsoft.com/develop/python/) SDK and the [azure-mgmt-compute package 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) to administer Managed Disks.</span></span> <span data-ttu-id="2be5c-109">Вы также можете создать вычислительный клиент, следуя инструкциям из [этого руководства](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagementcomputenetwork.html).</span><span class="sxs-lookup"><span data-stu-id="2be5c-109">You can create a compute client using this [tutorial](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagementcomputenetwork.html).</span></span>


## <a name="standalone-managed-disks"></a><span data-ttu-id="2be5c-110">Автономные управляемые диски</span><span class="sxs-lookup"><span data-stu-id="2be5c-110">Standalone Managed Disks</span></span>

<span data-ttu-id="2be5c-111">Вы можете легко создавать автономные управляемые диски несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="2be5c-111">You can easily create standalone Managed Disks in a variety of ways.</span></span>

### <a name="create-an-empty-managed-disk"></a><span data-ttu-id="2be5c-112">Создание пустого управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="2be5c-112">Create an empty Managed Disk.</span></span>
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

### <a name="create-a-managed-disk-from-blob-storage"></a><span data-ttu-id="2be5c-113">Создайте управляемый диск из хранилища BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="2be5c-113">Create a Managed Disk from Blob Storage.</span></span>
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

### <a name="create-a-managed-disk-from-your-own-image"></a><span data-ttu-id="2be5c-114">Создание управляемого диска из своего образа</span><span class="sxs-lookup"><span data-stu-id="2be5c-114">Create a Managed Disk from your own Image</span></span>
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

## <a name="virtual-machine-with-managed-disks"></a><span data-ttu-id="2be5c-115">Виртуальная машина с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="2be5c-115">Virtual Machine with Managed Disks</span></span>

<span data-ttu-id="2be5c-116">Вы можете создать виртуальную машину с неявным управляемым диском на основе определенного образа диска.</span><span class="sxs-lookup"><span data-stu-id="2be5c-116">You can create a Virtual Machine with an implicit Managed Disk for a specific disk image.</span></span> <span data-ttu-id="2be5c-117">Неявное создание управляемых дисков позволяет легко создавать диски, не указывая все сведения о них.</span><span class="sxs-lookup"><span data-stu-id="2be5c-117">Creation is simplified with implicit creation of managed disks without specifying all the disk details.</span></span> <span data-ttu-id="2be5c-118">Вам не нужно беспокоиться о создании учетных записей хранения и управлении ими.</span><span class="sxs-lookup"><span data-stu-id="2be5c-118">You do not have to worry about creating and managing Storage Accounts.</span></span>

<span data-ttu-id="2be5c-119">Управляемый диск создается неявно при создании виртуальной машины в Azure из образа ОС.</span><span class="sxs-lookup"><span data-stu-id="2be5c-119">A Managed Disk is created implicitly when creating VM from an OS image in Azure.</span></span> <span data-ttu-id="2be5c-120">Теперь для параметра ``storage_profile`` не обязательно указывать ``os_disk``, и создание учетной записи хранения не является обязательным требованием для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2be5c-120">In the ``storage_profile`` parameter, ``os_disk`` is now optional and you don't have to create a storage account as required precondition to create a Virtual Machine.</span></span>

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
<span data-ttu-id="2be5c-121">Указанный выше параметр ``storage_profile`` теперь считается допустимым.</span><span class="sxs-lookup"><span data-stu-id="2be5c-121">This ``storage_profile`` parameter is now valid.</span></span> <span data-ttu-id="2be5c-122">Полный пример создания виртуальной машины на Python (включая сеть и т. п.) см. в полном [руководстве по виртуальным машинам на Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span><span class="sxs-lookup"><span data-stu-id="2be5c-122">To get a complete example on how to create a VM in Python (including network, etc), check the full [VM tutorial in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span></span>

<span data-ttu-id="2be5c-123">Вы можете легко подключить ранее подготовленный управляемый диск.</span><span class="sxs-lookup"><span data-stu-id="2be5c-123">You can easily attach a previously provisioned Managed Disk.</span></span>
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

## <a name="virtual-machine-scale-sets-with-managed-disks"></a><span data-ttu-id="2be5c-124">Масштабируемые наборы виртуальных машин с управляемыми дисками.</span><span class="sxs-lookup"><span data-stu-id="2be5c-124">Virtual Machine Scale Sets with Managed Disks</span></span>

<span data-ttu-id="2be5c-125">До выпуска службы "Управляемые диски" вам нужно было вручную создавать учетную запись хранения для всех необходимых виртуальных машин в масштабируемом наборе, а затем в REST API этого набора указывать параметр списка ``vhd_containers``, чтобы предоставить всем виртуальным машинам имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="2be5c-125">Before Managed Disks, you needed to create a storage account manually for all the VMs you wanted inside your Scale Set, and then use the list parameter ``vhd_containers`` to provide all the storage account name to the Scale Set RestAPI.</span></span> <span data-ttu-id="2be5c-126">Официальное руководство по переходу доступно по этой ссылке: `article <https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span><span class="sxs-lookup"><span data-stu-id="2be5c-126">The official transition guide is available in this `article <https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`__.</span></span>

<span data-ttu-id="2be5c-127">Теперь благодаря управляемым дискам вы больше не будете иметь дела с учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="2be5c-127">Now with Managed Disk, you don't have to manage any storage account at all.</span></span> <span data-ttu-id="2be5c-128">Если вы часто используете пакет SDK для масштабируемого набора виртуальных машин для Python, можно использовать такое же значение параметра ``storage_profile``, как и при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2be5c-128">If you're are used to the VMSS Python SDK, your ``storage_profile`` can now be exactly the same as the one used in VM creation:</span></span>

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

<span data-ttu-id="2be5c-129">Полный пример кода:</span><span class="sxs-lookup"><span data-stu-id="2be5c-129">The full sample being:</span></span>

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

## <a name="other-operations-with-managed-disks"></a><span data-ttu-id="2be5c-130">Другие операции с управляемыми дисками</span><span class="sxs-lookup"><span data-stu-id="2be5c-130">Other Operations with Managed Disks</span></span>

### <a name="resizing-a-managed-disk"></a><span data-ttu-id="2be5c-131">Изменение размера управляемого диска</span><span class="sxs-lookup"><span data-stu-id="2be5c-131">Resizing a managed disk.</span></span>

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

### <a name="update-the-storage-account-type-of-the-managed-disks"></a><span data-ttu-id="2be5c-132">Обновление типа учетной записи хранения управляемых дисков</span><span class="sxs-lookup"><span data-stu-id="2be5c-132">Update the Storage Account type of the Managed Disks.</span></span>
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

### <a name="create-an-image-from-blob-storage"></a><span data-ttu-id="2be5c-133">Создание образа из хранилища BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="2be5c-133">Create an image from Blob Storage.</span></span>
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

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a><span data-ttu-id="2be5c-134">Создание моментального снимка управляемого диска, который сейчас подключен к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="2be5c-134">Create a snapshot of a Managed Disk that is currently attached to a Virtual Machine.</span></span>
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
