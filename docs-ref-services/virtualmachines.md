---
title: "Библиотеки виртуальных машин Azure для Python"
description: 
keywords: Azure, Python, SDK, API, Compute, Virtual Machines
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: c25665e19adb44c7112bf1533097ce1e6c739cb8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="8e65a-103">Библиотеки виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="8e65a-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="8e65a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8e65a-104">Overview</span></span>

<span data-ttu-id="8e65a-105">Выполняемые по запросу масштабируемые вычислительные ресурсы под управлением Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="8e65a-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="8e65a-106">Чтобы приступить к работе с виртуальными машинами Azure, см. инструкции по [созданию виртуальной машины Linux на портале Azure](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="8e65a-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="8e65a-107">API управления</span><span class="sxs-lookup"><span data-stu-id="8e65a-107">Management API</span></span>

<span data-ttu-id="8e65a-108">Создавайте, настраивайте, администрируйте и масштабируйте виртуальные машины Windows и Linux в Azure с использованием кода и API управления.</span><span class="sxs-lookup"><span data-stu-id="8e65a-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="8e65a-109">Установите библиотеку с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="8e65a-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a><span data-ttu-id="8e65a-110">Пример</span><span class="sxs-lookup"><span data-stu-id="8e65a-110">Example</span></span>

<span data-ttu-id="8e65a-111">Создание виртуальной машины Linux в существующей группе ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8e65a-111">Create a new Linux virtual machine in an existing Azure resource group.</span></span>

```python
VM_PARAMETERS={
        'location': 'LOCATION',
        'os_profile': {
            'computer_name': 'VM_NAME',
            'admin_username': 'USERNAME',
            'admin_password': 'PASSWORD'
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': 'Canonical',
                'offer': 'UbuntuServer',
                'sku': '16.04.0-LTS',
                'version': 'latest'
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': 'NIC_ID',
            }]
        },
    }

def create_vm()
    compute_client.virtual_machines.create_or_update(
        'RESOURCE_GROUP_NAME', 'VM_NAME', VM_PARAMETERS)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8e65a-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="8e65a-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a><span data-ttu-id="8e65a-113">Примеры</span><span class="sxs-lookup"><span data-stu-id="8e65a-113">Samples</span></span>

* <span data-ttu-id="8e65a-114">[Управление виртуальными машинами][1]</span><span class="sxs-lookup"><span data-stu-id="8e65a-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="8e65a-115">[Управление подсистемой балансировки нагрузки][2]</span><span class="sxs-lookup"><span data-stu-id="8e65a-115">[Manage a load balancer][2]</span></span>
* <span data-ttu-id="8e65a-116">[Создание и настройка управляемых дисков][3]</span><span class="sxs-lookup"><span data-stu-id="8e65a-116">[Create and configure managed disks][3]</span></span>
* <span data-ttu-id="8e65a-117">[Вывод списка образов][4]</span><span class="sxs-lookup"><span data-stu-id="8e65a-117">[List images][4]</span></span> 
* <span data-ttu-id="8e65a-118">[Мониторинг виртуальных машин][5]</span><span class="sxs-lookup"><span data-stu-id="8e65a-118">[Monitor virtual machines][5]</span></span>

<span data-ttu-id="8e65a-119">Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) примеров для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8e65a-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[3]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md