---
title: "Библиотеки Azure CDN для Python"
description: "Справочник по библиотекам Azure CDN для Python"
keywords: Azure, python, SDK, API, CDN
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: c704b32ff5fd6db922ef9c296142832455088562
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cdn-libraries-for-python"></a>Библиотеки Azure CDN для Python

## <a name="overview"></a>Обзор

[Сеть доставки содержимого Azure (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) предоставляет кэши веб-содержимого для обеспечения высокой пропускной способности по всему миру.

Чтобы приступить к работе с Azure CDN, см. инструкции по [началу работы с Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).

## <a name="management-apis"></a>API управления

Создание, запрашивание и администрирование сетей доставки содержимого Azure с помощью API управления.

Установите пакет управления с помощью pip.

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a>Пример

Создание профиля CDN, в котором определена одна конечная точка:

```python
from azure.mgmt.cdn import CdnManagementClient

cdn_client = CdnManagementClient(credentials, 'your-subscription-id')
profile_poller = cdn_client.profiles.create('my-resource-group',
                                            'cdn-name',
                                            {
                                                "location": "some_region", 
                                                "sku": {
                                                    "name": "sku_tier"
                                                } 
                                            })
profile = profile_poller.result()

endpoint_poller = client.endpoints.create('my-resource-group',
                                          'cdn-name',
                                          'unique-endpoint-name', 
                                          { 
                                              "location": "any_region", 
                                              "origins": [
                                                  {
                                                      "name": "origin_name", 
                                                      "host_name": "url"
                                                  }]
                                          })
endpoint = endpoint_poller.result()
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/cdn/managementlibrary)
