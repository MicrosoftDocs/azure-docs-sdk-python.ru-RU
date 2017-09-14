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
ms.openlocfilehash: f341e9066f48b35e182b4aba52b2f69e2b33e984
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/resources/managementlibrary)

## <a name="samples"></a>Примеры
[Manage Azure resources and resource groups with .NET (Управление ресурсами и группами ресурсов Azure с помощью .NET)](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

См. [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) примеров для Azure Resource Manager.
