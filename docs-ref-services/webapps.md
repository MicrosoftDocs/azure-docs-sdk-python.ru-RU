---
title: "Библиотеки веб-приложений Azure для Python"
description: 
keywords: Azure, Python, SDK, API, web apps, App Service
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 05f6ad173f4ec051654b5eb2a986b2c2a93cc33a
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-web-apps-libraries-for-python"></a>Библиотеки веб-приложений Azure для Python

## <a name="overview"></a>Обзор

[Служба приложений Azure](/azure/app-service) позволяет развертывать и масштабировать веб-сайты, веб-приложения, службы и интерфейсы REST API.

Чтобы приступить к работе со службой приложений Azure, см. инструкции по [созданию веб-приложения Python в Azure](/azure/app-service-web/app-service-web-get-started-python).

## <a name="management-api"></a>API управления

Развертывайте и масштабируйте элементы, размещенные в службе приложений Azure, а также управляйте ими с помощью API управления.

Установите библиотеку с помощью pip.

```bash
pip install azure-mgmt-web
```

### <a name="example"></a>Пример

Развертывание веб-приложения из репозитория GitHub в веб-приложении Azure.

```python
siteConfiguration = SiteConfig(
    python_version='3.4'
)

# create a web app
web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=SERVICE_PLAN_ID,
        site_config=siteConfiguration
    )
)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url='https://github.com/lisawong19/python-docs-hello-world',
        branch='master'
    )
)
```
> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/webapps/managementlibrary)

## <a name="samples"></a>Примеры 

* [Управление веб-сайтами Azure с помощью Python][1]
* [Создание рабочего процесса приложения логики][2]
 
Просмотрите [полный список](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) примеров веб-приложений.

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md