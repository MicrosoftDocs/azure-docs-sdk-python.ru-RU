---
title: Библиотеки службы "Фабрика данных Azure" для Python
description: Справочник по библиотекам службы "Фабрика данных Azure" для Python
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 05/10/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 05d93f7d1838c110c3ba77f7abd3967f7870774b
ms.sourcegitcommit: d65549030a0edb50d75482f79aac0962d1dacb57
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34759055"
---
# <a name="azure-data-factory-libraries-for-python"></a><span data-ttu-id="bc668-103">Библиотеки службы "Фабрика данных Azure" для Python</span><span class="sxs-lookup"><span data-stu-id="bc668-103">Azure Data Factory libraries for Python</span></span>

<span data-ttu-id="bc668-104">Объедините службы хранения, перемещения и обработки данных в автоматизированные конвейеры данных с помощью службы [Фабрика данных Azure](/azure/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="bc668-104">Compose data storage, movement, and processing services into automated data pipelines with [Azure Data Factory](/azure/data-factory/)</span></span>

<span data-ttu-id="bc668-105">См. дополнительные сведения о [службе "Фабрика данных"](/azure/data-factory/introduction) и начните работу с ней с помощью руководства [Создание фабрики данных и конвейера с помощью Python](/azure/data-factory/quickstart-create-data-factory-python).</span><span class="sxs-lookup"><span data-stu-id="bc668-105">[Learn more](/azure/data-factory/introduction) about Data Factory and get started with the [Create a data factory and pipeline using Python quickstart](/azure/data-factory/quickstart-create-data-factory-python).</span></span> 

## <a name="management-module"></a><span data-ttu-id="bc668-106">Модуль управления</span><span class="sxs-lookup"><span data-stu-id="bc668-106">Management module</span></span>

<span data-ttu-id="bc668-107">Создавайте и администрируйте ресурсы службы "Фабрика данных" в своей подписке с помощью модуля управления.</span><span class="sxs-lookup"><span data-stu-id="bc668-107">Create and manage Data Factory instances in your subscription with the management module.</span></span>

### <a name="installation"></a><span data-ttu-id="bc668-108">Установка</span><span class="sxs-lookup"><span data-stu-id="bc668-108">Installation</span></span>

<span data-ttu-id="bc668-109">Установите пакет с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="bc668-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-datafactory 
```

### <a name="example"></a><span data-ttu-id="bc668-110">Пример</span><span class="sxs-lookup"><span data-stu-id="bc668-110">Example</span></span> 

<span data-ttu-id="bc668-111">Создайте службу "Фабрика данных" в подписке в регионе "Восток США".</span><span class="sxs-lookup"><span data-stu-id="bc668-111">Create a Data Factory in your subscription on the East US region.</span></span>

```python
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.datafactory import DataFactoryManagementClient
from azure.mgmt.datafactory.models import *
import time

#Create a data factory
subscription_id = '<Specify your Azure Subscription ID>'
credentials = ServicePrincipalCredentials(client_id='<Active Directory application/client ID>', secret='<client secret>', tenant='<Active Directory tenant ID>')
adf_client = DataFactoryManagementClient(credentials, subscription_id)

rg_params = {'location':'eastus'}
df_params = {'location':'eastus'}  

df_resource = Factory(location='eastus')
df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
print_item(df)
while df.provisioning_state != 'Succeeded':
    df = adf_client.factories.get(rg_name, df_name)
    time.sleep(1)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc668-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="bc668-112">Explore the Management APIs</span></span>](/python/api/overview/azure/datafactory/management)