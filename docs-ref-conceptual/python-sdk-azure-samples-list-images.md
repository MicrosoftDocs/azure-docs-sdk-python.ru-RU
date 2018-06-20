---
title: Вывод списка образов
description: Просмотр всех доступных образов для создания виртуальных машин.
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: b0c640a090657128c7d7a97174f0eed036d0d9dd
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
ms.locfileid: "20909037"
---
# <a name="list-images"></a><span data-ttu-id="97423-103">Вывод списка образов</span><span class="sxs-lookup"><span data-stu-id="97423-103">List images</span></span>

<span data-ttu-id="97423-104">Используйте следующий код для вывода всех доступных образов для создания виртуальных машин, включая все номера SKU и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97423-104">Use the following code to print all of the available images to use for creating virtual machines, including all skus and versions.</span></span>

```python
region = 'eastus'

result_list_pub = compute_client.virtual_machine_images.list_publishers(
    region,
)

for publisher in result_list_pub:
    result_list_offers = compute_client.virtual_machine_images.list_offers(
        region,
        publisher.name,
    )

    for offer in result_list_offers:
        result_list_skus = compute_client.virtual_machine_images.list_skus(
            region,
            publisher.name,
            offer.name,
        )

        for sku in result_list_skus:
            result_list = compute_client.virtual_machine_images.list(
                region,
                publisher.name,
                offer.name,
                sku.name,
            )

            for version in result_list:
                result_get = compute_client.virtual_machine_images.get(
                    region,
                    publisher.name,
                    offer.name,
                    sku.name,
                    version.name,
                )

                print('PUBLISHER: {0}, OFFER: {1}, SKU: {2}, VERSION: {3}'.format(
                    publisher.name,
                    offer.name,
                    sku.name,
                    version.name,
                ))
```
