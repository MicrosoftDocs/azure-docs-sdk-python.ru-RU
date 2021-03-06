---
title: Библиотеки виртуальных машин Azure для Python
description: ''
keywords: Azure, Python, SDK, API, Compute, Virtual Machines
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: e09ffed98f3f6050e34ca2cb39e645e30f8bdb15
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534187"
---
# <a name="azure-virtual-machine-libraries"></a>Библиотеки виртуальных машин Azure

## <a name="overview"></a>Обзор

Выполняемые по запросу масштабируемые вычислительные ресурсы под управлением Windows или Linux.

Чтобы приступить к работе с виртуальными машинами Azure, см. инструкции по [созданию виртуальной машины Linux на портале Azure](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>API управления

Создавайте, настраивайте, администрируйте и масштабируйте виртуальные машины Windows и Linux в Azure с использованием кода и API управления.

Установите библиотеку с помощью pip.

```bash
pip install azure-mgmt-compute
```

### <a name="example"></a>Пример

Создайте виртуальную машину Linux в существующей группе ресурсов Azure с использованием аутентификации на основе удостоверения управляемой службы (MSI).

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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a>Примеры

* [Управление виртуальными машинами][1]
* [Аутентификация с использованием Управляемого удостоверения службы][2]
* [Создание виртуальной машины с помощью расширения Управляемого удостоверения службы][3]
* [Управление подсистемой балансировки нагрузки][4]
* [Создание и настройка управляемых дисков][5]
* [Вывод списка образов][6] 
* [Мониторинг виртуальных машин][7]

Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) примеров для виртуальных машин.

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md
