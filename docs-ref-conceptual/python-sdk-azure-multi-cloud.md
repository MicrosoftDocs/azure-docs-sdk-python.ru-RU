---
title: Многоблачные решения
description: Использование Azure во всех регионах
author: lmazuel
ms.author: lmazuel
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: a4d006e6244bf6fb1151e32583e8bc3a642d4663
ms.sourcegitcommit: 8a9e4295359a4f47b21908541e2460c333e94a0a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/08/2018
ms.locfileid: "39624980"
---
# <a name="multi-cloud---use-azure-on-all-regions"></a><span data-ttu-id="a5da2-103">Многооблачные решения. Использование Azure во всех регионах</span><span class="sxs-lookup"><span data-stu-id="a5da2-103">Multi-cloud - use Azure on all regions</span></span>

<span data-ttu-id="a5da2-104">Пакет Azure SDK для Python можно использовать для подключения ко всем регионам с [доступом](https://azure.microsoft.com/regions/services) к Azure.</span><span class="sxs-lookup"><span data-stu-id="a5da2-104">You can use the Azure SDK for Python to connect to all regions where Azure is [available](https://azure.microsoft.com/regions/services).</span></span>

<span data-ttu-id="a5da2-105">По умолчанию пакет Azure SDK для Python настраивается для подключения к общедоступным ресурсам Azure.</span><span class="sxs-lookup"><span data-stu-id="a5da2-105">By default, the Azure SDK for Python is configured to connect to public Azure.</span></span>

## <a name="using-predeclared-cloud-definition"></a><span data-ttu-id="a5da2-106">Использование предварительно объявленного определения облака</span><span class="sxs-lookup"><span data-stu-id="a5da2-106">Using predeclared cloud definition</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5da2-107">Пакет `msrestazure` должен иметь версию 0.4.11 или выше для этого раздела.</span><span class="sxs-lookup"><span data-stu-id="a5da2-107">The `msrestazure` package must be superior or equals to 0.4.11 for this section.</span></span>

<span data-ttu-id="a5da2-108">Можно использовать модуль `azure_cloud` `msrestazure`.</span><span class="sxs-lookup"><span data-stu-id="a5da2-108">You can use the `azure_cloud` module of `msrestazure`</span></span>

```python
from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=AZURE_CHINA_CLOUD
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager
)
``` 
  
<span data-ttu-id="a5da2-109">Доступные определения облаков:</span><span class="sxs-lookup"><span data-stu-id="a5da2-109">Available cloud definition are</span></span>
  - <span data-ttu-id="a5da2-110">AZURE_PUBLIC_CLOUD</span><span class="sxs-lookup"><span data-stu-id="a5da2-110">AZURE_PUBLIC_CLOUD</span></span>
  - <span data-ttu-id="a5da2-111">AZURE_CHINA_CLOUD</span><span class="sxs-lookup"><span data-stu-id="a5da2-111">AZURE_CHINA_CLOUD</span></span>
  - <span data-ttu-id="a5da2-112">AZURE_US_GOV_CLOUD</span><span class="sxs-lookup"><span data-stu-id="a5da2-112">AZURE_US_GOV_CLOUD</span></span>
  - <span data-ttu-id="a5da2-113">AZURE_GERMAN_CLOUD</span><span class="sxs-lookup"><span data-stu-id="a5da2-113">AZURE_GERMAN_CLOUD</span></span>

## <a name="using-your-own-cloud-definition-eg-azure-stack"></a><span data-ttu-id="a5da2-114">Использование собственного определения облака (например Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="a5da2-114">Using your own cloud definition (e.g. Azure Stack)</span></span>
<span data-ttu-id="a5da2-115">ARM имеет вспомогательную конечную точку метаданных:</span><span class="sxs-lookup"><span data-stu-id="a5da2-115">ARM has a metadata endpoint to help you:</span></span>

```python
from msrestazure.azure_cloud import get_cloud_from_metadata_endpoint
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

mystack_cloud = get_cloud_from_metadata_endpoint("https://myazurestack-arm-endpoint.com")
credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=mystack_cloud
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=mystack_cloud.endpoints.resource_manager
)
```
## <a name="using-adal"></a><span data-ttu-id="a5da2-116">Использование ADAL</span><span class="sxs-lookup"><span data-stu-id="a5da2-116">Using ADAL</span></span>

<span data-ttu-id="a5da2-117">Для подключения к другому региону, нужно учитывать следующее:</span><span class="sxs-lookup"><span data-stu-id="a5da2-117">To connect to another region, a few things have to be considered:</span></span>

- <span data-ttu-id="a5da2-118">Какая конечная точка используется для запроса маркера (для аутентификации)?</span><span class="sxs-lookup"><span data-stu-id="a5da2-118">What is the endpoint where to ask for a token (authentication)?</span></span>
- <span data-ttu-id="a5da2-119">Какая конечная точка используется для этого маркера (для применения)?</span><span class="sxs-lookup"><span data-stu-id="a5da2-119">What is the endpoint where I will use this token (usage)?</span></span>

<span data-ttu-id="a5da2-120">Общий пример:</span><span class="sxs-lookup"><span data-stu-id="a5da2-120">This is a generic example:</span></span>

```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Public Azure - default values
authentication_endpoint = 'https://login.microsoftonline.com/'
azure_endpoint = 'https://management.azure.com/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-government"></a><span data-ttu-id="a5da2-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="a5da2-121">Azure Government</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Government
authentication_endpoint = 'https://login.microsoftonline.us/'
azure_endpoint = 'https://management.usgovcloudapi.net/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-germany"></a><span data-ttu-id="a5da2-122">Azure для Германии</span><span class="sxs-lookup"><span data-stu-id="a5da2-122">Azure Germany</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Azure Germany
authentication_endpoint = 'https://login.microsoftonline.de/'
azure_endpoint = 'https://management.microsoftazure.de/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-china"></a><span data-ttu-id="a5da2-123">Azure для Китая</span><span class="sxs-lookup"><span data-stu-id="a5da2-123">Azure China</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Azure China
authentication_endpoint = 'https://login.chinacloudapi.cn/'
azure_endpoint = 'https://management.chinacloudapi.cn/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```
