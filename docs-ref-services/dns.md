---
title: "Библиотеки Azure DNS для Python"
description: "Справочник по библиотекам Azure DNS для Python"
keywords: Azure, python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 59ae3628b4a810db8fee21aacf46c13054dc8cd3
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-dns-libraries-for-python"></a>Библиотеки Azure DNS для Python

## <a name="overview"></a>Обзор

[Azure DNS](/azure/dns/dns-overview) — это служба размещения для доменов DNS, которая предоставляет разрешение имен DNS с помощью инфраструктуры Azure.

Чтобы приступить к работе с Azure DNS, см. инструкции по [началу работы с Azure DNS с помощью портала Azure](/azure/dns/dns-getstarted-portal).

## <a name="management-apis"></a>API управления

Создание зон и записей DNS, а также управление ими с помощью API управления.

Установите пакет управления с помощью pip.

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a>Пример

Создание зоны DNS.

```python
from azure.mgmt.dns import DnsManagementClient

dns_client = DnsManagementClient(credentials, 'your-subscription-id')
zone = dns_client.zones.create_or_update('resource-group',
                                         'zone_name_no_dot',
                                         {
                                            "location": "global"
                                         })

```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/dns/managementlibrary)
