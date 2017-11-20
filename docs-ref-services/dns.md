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
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="0e401-104">Библиотеки Azure DNS для Python</span><span class="sxs-lookup"><span data-stu-id="0e401-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="0e401-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="0e401-105">Overview</span></span>

<span data-ttu-id="0e401-106">[Azure DNS](/azure/dns/dns-overview) — это служба размещения для доменов DNS, которая предоставляет разрешение имен DNS с помощью инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="0e401-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="0e401-107">Чтобы приступить к работе с Azure DNS, см. инструкции по [началу работы с Azure DNS с помощью портала Azure](/azure/dns/dns-getstarted-portal).</span><span class="sxs-lookup"><span data-stu-id="0e401-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="0e401-108">API управления</span><span class="sxs-lookup"><span data-stu-id="0e401-108">Management APIs</span></span>

<span data-ttu-id="0e401-109">Создание зон и записей DNS, а также управление ими с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="0e401-109">Create and manage DNS zones and records with the management API.</span></span>

<span data-ttu-id="0e401-110">Установите пакет управления с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="0e401-110">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a><span data-ttu-id="0e401-111">Пример</span><span class="sxs-lookup"><span data-stu-id="0e401-111">Example</span></span>

<span data-ttu-id="0e401-112">Создание зоны DNS.</span><span class="sxs-lookup"><span data-stu-id="0e401-112">Create a new DNS zone.</span></span>

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
> [<span data-ttu-id="0e401-113">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="0e401-113">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/managementlibrary)
