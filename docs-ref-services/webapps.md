---
title: Библиотеки веб-приложений Azure для Python
description: ''
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
ms.openlocfilehash: 4870394c6ee39cde546d090fa1a0d136609851b3
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376698"
---
# <a name="azure-web-apps-libraries-for-python"></a><span data-ttu-id="3c0f7-103">Библиотеки веб-приложений Azure для Python</span><span class="sxs-lookup"><span data-stu-id="3c0f7-103">Azure Web Apps libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="3c0f7-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3c0f7-104">Overview</span></span>

<span data-ttu-id="3c0f7-105">[Служба приложений Azure](/azure/app-service) позволяет развертывать и масштабировать веб-сайты, веб-приложения, службы и интерфейсы REST API.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-105">Deploy and scale websites, web applications, services, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="3c0f7-106">Чтобы приступить к работе со службой приложений Azure, см. инструкции по [созданию веб-приложения Python в Azure](/azure/app-service-web/app-service-web-get-started-python).</span><span class="sxs-lookup"><span data-stu-id="3c0f7-106">To get started with Azure App Service, see [Create a Python web app in Azure](/azure/app-service-web/app-service-web-get-started-python).</span></span>

## <a name="management-api"></a><span data-ttu-id="3c0f7-107">API управления</span><span class="sxs-lookup"><span data-stu-id="3c0f7-107">Management API</span></span>

<span data-ttu-id="3c0f7-108">Развертывайте и масштабируйте элементы, размещенные в службе приложений Azure, а также управляйте ими с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-108">Deploy, manage, and scale elements hosted in the Azure App Service with the management API.</span></span>

<span data-ttu-id="3c0f7-109">Установите библиотеку с помощью pip.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-web
```

### <a name="example"></a><span data-ttu-id="3c0f7-110">Пример</span><span class="sxs-lookup"><span data-stu-id="3c0f7-110">Example</span></span>

<span data-ttu-id="3c0f7-111">Развертывание веб-приложения из репозитория GitHub в веб-приложении Azure.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-111">Deploy a webapp from a GitHub repository into Azure Web App.</span></span>

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
> [<span data-ttu-id="3c0f7-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="3c0f7-112">Explore the Management APIs</span></span>](/python/api/overview/azure/webapps/management)

## <a name="samples"></a><span data-ttu-id="3c0f7-113">Примеры</span><span class="sxs-lookup"><span data-stu-id="3c0f7-113">Samples</span></span>

* <span data-ttu-id="3c0f7-114">[Управление веб-сайтами Azure с помощью Python][1]</span><span class="sxs-lookup"><span data-stu-id="3c0f7-114">[Manage Azure websites with python][1]</span></span>
* <span data-ttu-id="3c0f7-115">[Создание рабочего процесса приложения логики][2]</span><span class="sxs-lookup"><span data-stu-id="3c0f7-115">[Create a Logic App workflow][2]</span></span>

<span data-ttu-id="3c0f7-116">Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=web-app) примеров веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="3c0f7-116">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=web-app) of web application samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md
