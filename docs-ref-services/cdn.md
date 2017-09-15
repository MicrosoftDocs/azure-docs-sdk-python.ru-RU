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
# <a name="azure-cdn-libraries-for-python"></a><span data-ttu-id="8f1eb-104">Библиотеки Azure CDN для Python</span><span class="sxs-lookup"><span data-stu-id="8f1eb-104">Azure CDN libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="8f1eb-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="8f1eb-105">Overview</span></span>

<span data-ttu-id="8f1eb-106">[Сеть доставки содержимого Azure (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) предоставляет кэши веб-содержимого для обеспечения высокой пропускной способности по всему миру.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-106">[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) allows you to provide web content caches to ensure high-bandwidth availability across the globe.</span></span>

<span data-ttu-id="8f1eb-107">Чтобы приступить к работе с Azure CDN, см. инструкции по [началу работы с Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="8f1eb-107">To get started with Azure CDN, see [Getting started with Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-apis"></a><span data-ttu-id="8f1eb-108">API управления</span><span class="sxs-lookup"><span data-stu-id="8f1eb-108">Management APIs</span></span>

<span data-ttu-id="8f1eb-109">Создание, запрашивание и администрирование сетей доставки содержимого Azure с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-109">Create, query, and manage Azure CDNs with the management API.</span></span>

<span data-ttu-id="8f1eb-110">Установите пакет управления с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-110">Install the management package via pip.</span></span>

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a><span data-ttu-id="8f1eb-111">Пример</span><span class="sxs-lookup"><span data-stu-id="8f1eb-111">Example</span></span>

<span data-ttu-id="8f1eb-112">Создание профиля CDN, в котором определена одна конечная точка:</span><span class="sxs-lookup"><span data-stu-id="8f1eb-112">Creating a CDN profile with a single defined endpoint:</span></span>

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
> [<span data-ttu-id="8f1eb-113">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="8f1eb-113">Explore the Management APIs</span></span>](/python/api/overview/azure/cdn/managementlibrary)