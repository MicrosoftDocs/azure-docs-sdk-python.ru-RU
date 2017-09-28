---
title: "Библиотеки ресурсов Azure для Python"
description: "Справочник по библиотекам ресурсов Azure для Python"
keywords: Azure, python, SDK, API, Resources
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: d8a27bc2b5480b07728a0b3f892f5c3c70c913d9
ms.sourcegitcommit: 427b44319ae99bf19e167f427e7681b2103dd8e4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2017
---
# <a name="azure-resources-libraries-for-python"></a>Библиотеки ресурсов Azure для Python

## <a name="overview"></a>Обзор 
Развертывайте, отслеживайте и администрируйте ресурсы в группах с помощью [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API управления
Используйте API управления для создания групп ресурсов и развертывания ресурсов на основе шаблонов.

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a>Пример 
Создайте группу ресурсов в следующем регионе Azure: восточная часть США.

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagmentClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a>Примеры
[Manage Azure resources and resource groups with .NET (Управление ресурсами и группами ресурсов Azure с помощью .NET)](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

См. [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) примеров для Azure Resource Manager.
