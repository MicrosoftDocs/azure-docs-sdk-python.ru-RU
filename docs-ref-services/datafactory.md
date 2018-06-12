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
# <a name="azure-data-factory-libraries-for-python"></a>Библиотеки службы "Фабрика данных Azure" для Python

Объедините службы хранения, перемещения и обработки данных в автоматизированные конвейеры данных с помощью службы [Фабрика данных Azure](/azure/data-factory/).

См. дополнительные сведения о [службе "Фабрика данных"](/azure/data-factory/introduction) и начните работу с ней с помощью руководства [Создание фабрики данных и конвейера с помощью Python](/azure/data-factory/quickstart-create-data-factory-python). 

## <a name="management-module"></a>Модуль управления

Создавайте и администрируйте ресурсы службы "Фабрика данных" в своей подписке с помощью модуля управления.

### <a name="installation"></a>Установка

Установите пакет с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-mgmt-datafactory 
```

### <a name="example"></a>Пример 

Создайте службу "Фабрика данных" в подписке в регионе "Восток США".

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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/datafactory/management)