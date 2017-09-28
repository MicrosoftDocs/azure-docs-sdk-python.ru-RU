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
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="c4746-104">Библиотеки ресурсов Azure для Python</span><span class="sxs-lookup"><span data-stu-id="c4746-104">Azure Resources libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="c4746-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="c4746-105">Overview</span></span> 
<span data-ttu-id="c4746-106">Развертывайте, отслеживайте и администрируйте ресурсы в группах с помощью [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="c4746-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="c4746-107">API управления</span><span class="sxs-lookup"><span data-stu-id="c4746-107">Management API</span></span>
<span data-ttu-id="c4746-108">Используйте API управления для создания групп ресурсов и развертывания ресурсов на основе шаблонов.</span><span class="sxs-lookup"><span data-stu-id="c4746-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a><span data-ttu-id="c4746-109">Пример</span><span class="sxs-lookup"><span data-stu-id="c4746-109">Example</span></span> 
<span data-ttu-id="c4746-110">Создайте группу ресурсов в следующем регионе Azure: восточная часть США.</span><span class="sxs-lookup"><span data-stu-id="c4746-110">Create a new resource group in the Azure Eastern US region.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagmentClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4746-111">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="c4746-111">Explore the Management APIs</span></span>](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a><span data-ttu-id="c4746-112">Примеры</span><span class="sxs-lookup"><span data-stu-id="c4746-112">Samples</span></span>
[<span data-ttu-id="c4746-113">Manage Azure resources and resource groups with .NET (Управление ресурсами и группами ресурсов Azure с помощью .NET)</span><span class="sxs-lookup"><span data-stu-id="c4746-113">Manage Azure resources and resource groups</span></span>](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

<span data-ttu-id="c4746-114">См. [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) примеров для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4746-114">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) of Azure Resource Manager samples.</span></span>
