---
title: Библиотеки Azure CDN для Python
description: Справочник по библиотекам Azure CDN для Python
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
ms.openlocfilehash: 2dd7703e94a814d85716a7b96994666e32f95565
ms.sourcegitcommit: 3db75daa592da90ea9aa8fd17fb99627a30eb4fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/23/2019
ms.locfileid: "66179869"
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

endpoint_poller = cdn_client.endpoints.create('my-resource-group',
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
> [Обзор API-интерфейсов управления](/python/api/overview/azure/cdn/management)
