---
title: Библиотеки ресурсов Azure для Python
description: ''
keywords: Azure, Python, SDK, API, Resources
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: d708a5e7296b166b6e55b9b7b0d995e72e264267
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534370"
---
# <a name="azure-resources-libraries-for-python"></a>Библиотеки ресурсов Azure для Python 

## <a name="overview"></a>Обзор 
Управление ресурсами Azure в группах ресурсов.

| Package  |  ОПИСАНИЕ |
|---|---|
|[azure.mgmt.resource.features][1]|Azure Feature Exposure Control (AFEC) — это механизм для поставщиков ресурсов, который обеспечивает контроль над отображением функций пользователям.|
|[azure.mgmt.resource.links][2]|Ресурсы Azure можно связывать друг с другом, формируя логические связи. Связи можно устанавливать между ресурсами, принадлежащими к разным группам ресурсов.|
|[azure.mgmt.resource.locks][3]|Ресурсы Azure можно блокировать, чтобы другие пользователи из вашей организации не могли их удалить или изменить.|
|[azure.mgmt.resource.managedapplications][4]|Приложения (устройства), управляемые с помощью ARM.|
|[azure.mgmt.resource.policy][5]|Для управления доступом к ресурсам и контроля над ним можно определить настраиваемые политики и назначить их в той или иной области.|
|[azure.mgmt.resource.resources][6]| Операции для работы с ресурсами и группами ресурсов.|
|[azure.mgmt.resource.subscriptions][7]|Все ресурсы и группы ресурсов существуют в пределах подписок. Эти операции позволяют получать сведения о подписках и клиентах.|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a>Установка библиотек 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a>Пример
Ниже приведен пример создания группы ресурсов. 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

Ознакомьтесь с другими [примерами кода Python](https://azure.microsoft.com/resources/samples/?platform=python), которые можно использовать в приложениях. 