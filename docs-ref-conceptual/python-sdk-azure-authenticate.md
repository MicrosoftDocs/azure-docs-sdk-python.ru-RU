---
title: Проверка подлинности с помощью библиотек управления Azure для Python
description: Проверка подлинности с помощью субъекта-службы в библиотеках управления Azure для Python
keywords: Azure, Python, SDK, API, authentication, active directory, service principal
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/24/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 78b248071e4718c1ab5ad743e697eafcfb510ec5
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/18/2018
ms.locfileid: "35720055"
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a><span data-ttu-id="92062-104">Проверка подлинности с помощью библиотек управления Azure для Python</span><span class="sxs-lookup"><span data-stu-id="92062-104">Authenticate with the Azure Management Libraries for Python</span></span>

<span data-ttu-id="92062-105">Существует несколько способов проверки подлинности приложения с помощью библиотек управления Azure для Python при создании ресурсов и управления ими.</span><span class="sxs-lookup"><span data-stu-id="92062-105">Several options are available to authenticate your application with Azure when using the Python management libraries to create and manage resources.</span></span>

## <a name="mgmt-auth-token"></a><span data-ttu-id="92062-106">Проверка подлинности с использованием учетных данных токена</span><span class="sxs-lookup"><span data-stu-id="92062-106">Authenticate with token credentials</span></span>

<span data-ttu-id="92062-107">Учетные данные можно безопасно хранить в файле конфигурации, реестре или Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="92062-107">Store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

<span data-ttu-id="92062-108">В следующем примере для проверки подлинности используется [субъект-служба](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="92062-108">The following example uses a [Service Principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) for authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="92062-109">Вы можете создать субъект-службу с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="92062-109">You can create a Service Principal via the Azure CLI 2.0</span></span>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```

```python
    from azure.common.credentials import ServicePrincipalCredentials

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    credentials = ServicePrincipalCredentials(
        client_id = CLIENT,
        secret = KEY,
        tenant = TENANT_ID
    )
```

> <span data-ttu-id="92062-110">[Примечание.] Чтобы подключиться к одному из независимых облаков Azure, используйте параметр `cloud_environment`.</span><span class="sxs-lookup"><span data-stu-id="92062-110">[NOTE!] To connect to one of the Azure sovereign clouds, use the `cloud_environment` parameter.</span></span>

```python
    from azure.common.credentials import ServicePrincipalCredentials
    from msrestazure.azure_cloud import AZURE_CHINA_CLOUD

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    credentials = ServicePrincipalCredentials(
        client_id = CLIENT,
        secret = KEY,
        tenant = TENANT_ID,
        cloud_environment = AZURE_CHINA_CLOUD
    )
```

<span data-ttu-id="92062-111">Если требуется более строгий контроль, рекомендуем использовать [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) и программу-оболочку ADAL для SDK.</span><span class="sxs-lookup"><span data-stu-id="92062-111">If you need more control, it is recommended to use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) and the SDK ADAL wrapper.</span></span> <span data-ttu-id="92062-112">Список всех доступных сценариев и примеры см. на веб-сайте ADAL.</span><span class="sxs-lookup"><span data-stu-id="92062-112">Please refer to the ADAL website for all the available scenarios list and samples.</span></span> <span data-ttu-id="92062-113">Пример проверки подлинности на основе субъекта-службы:</span><span class="sxs-lookup"><span data-stu-id="92062-113">For instance for service principal authentication:</span></span>

```python
    import adal
    from msrestazure.azure_active_directory import AdalAuthentication
    from msrestazure.azure_cloud import AZURE_PUBLIC_CLOUD

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    LOGIN_ENDPOINT = AZURE_PUBLIC_CLOUD.endpoints.active_directory
    RESOURCE = AZURE_PUBLIC_CLOUD.endpoints.active_directory_resource_id

    context = adal.AuthenticationContext(LOGIN_ENDPOINT + '/' + TENANT_ID)
    credentials = AdalAuthentication(
        context.acquire_token_with_client_credentials,
        RESOURCE,
        CLIENT,
        KEY
    )
```

<span data-ttu-id="92062-114">Все допустимые вызовы ADAL можно использовать с классом `AdalAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="92062-114">All ADAL valid calls can be used with the `AdalAuthentication` class.</span></span>

<span data-ttu-id="92062-115">Затем создайте клиентский объект, чтобы приступить к работе с API.</span><span class="sxs-lookup"><span data-stu-id="92062-115">Next, create a client object to start working with the API:</span></span>

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> <span data-ttu-id="92062-116">[Примечание.] Если используется независимое облако Azure, при создании клиента управления необходимо также указать соответствующий базовый URL-адрес (используя константы в `msrestazure.azure_cloud`).</span><span class="sxs-lookup"><span data-stu-id="92062-116">[NOTE!] When using an Azure sovereign cloud you must also specify the appropriate base URL (via the constants in `msrestazure.azure_cloud`) when creating the management client.</span></span> <span data-ttu-id="92062-117">Пример для облака Azure для Китая:</span><span class="sxs-lookup"><span data-stu-id="92062-117">For example for Azure China Cloud:</span></span>
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
> ```


## <a name="mgmt-auth-file"></a><span data-ttu-id="92062-118">Проверка подлинности на основе файлов</span><span class="sxs-lookup"><span data-stu-id="92062-118">File based authentication</span></span>

<span data-ttu-id="92062-119">Самый простой способ реализовать проверку подлинности — создать JSON-файл, который содержит учетные данные для субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="92062-119">The simplest way to authenticate is to create a JSON file that contains credentials for an Azure Service Principal.</span></span> <span data-ttu-id="92062-120">Вы можете одновременно создать субъект-службу и этот файл с помощью следующей команды интерфейса командной строки:</span><span class="sxs-lookup"><span data-stu-id="92062-120">You can use the following CLI command to create a new Service Principal and this file at the same time:</span></span>

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

<span data-ttu-id="92062-121">Сохраните этот файл в безопасном расположении в вашей системе, доступном для кода.</span><span class="sxs-lookup"><span data-stu-id="92062-121">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="92062-122">Задайте переменную среды и укажите полный путь к файлу в оболочке:</span><span class="sxs-lookup"><span data-stu-id="92062-122">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

<span data-ttu-id="92062-123">Если вы хотите создать файл самостоятельно, придерживайтесь следующего формата:</span><span class="sxs-lookup"><span data-stu-id="92062-123">If you want to create the file yourself, please follow this format:</span></span>

```json
{
    "clientId": "ad735158-65ca-11e7-ba4d-ecb1d756380e",
    "clientSecret": "b70bb224-65ca-11e7-810c-ecb1d756380e",
    "subscriptionId": "bfc42d3a-65ca-11e7-95cf-ecb1d756380e",
    "tenantId": "c81da1d8-65ca-11e7-b1d1-ecb1d756380e",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="92062-124">Затем можно создать любой клиент с помощью фабрики клиента.</span><span class="sxs-lookup"><span data-stu-id="92062-124">You can then create any client using the client factory:</span></span>
```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a><span data-ttu-id="92062-125">Аутентификация на основе удостоверения управляемой службы (MSI)</span><span class="sxs-lookup"><span data-stu-id="92062-125">Authenticate with Managed Service Identity(MSI)</span></span> 
<span data-ttu-id="92062-126">MSI позволяет ресурсу в Azure использовать пакет SDK или CLI без необходимости создать соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="92062-126">MSI is a simple way for a resource in Azure to use SDK/CLI without the need to create specific credentials.</span></span>

```python
from msrestazure.azure_active_directory import MSIAuthentication
from azure.mgmt.resource import ResourceManagementClient, SubscriptionClient

    # Create MSI Authentication
    credentials = MSIAuthentication()


    # Create a Subscription Client
    subscription_client = SubscriptionClient(credentials)
    subscription = next(subscription_client.subscriptions.list())
    subscription_id = subscription.subscription_id

    # Create a Resource Management client
    resource_client = ResourceManagementClient(credentials, subscription_id)

    
    # List resource groups as an example. The only limit is what role and policy are assigned to this MSI token.
    for resource_group in resource_client.resource_groups.list():
        print(resource_group.name)

```

## <a name="mgmt-auth-cli"></a><span data-ttu-id="92062-127">Проверка подлинности на основе интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="92062-127">CLI-based authentication</span></span>

<span data-ttu-id="92062-128">Пакет SDK позволяет создать клиент, используя активную подписку CLI.</span><span class="sxs-lookup"><span data-stu-id="92062-128">The SDK is able to create a client using your CLI active subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92062-129">Эти инструкции следует применять в качестве краткого руководства по разработке.</span><span class="sxs-lookup"><span data-stu-id="92062-129">This should be used as quick start developer experience.</span></span> <span data-ttu-id="92062-130">В рабочей среде используйте [ADAL](#authenticate-with-token-credentials) или свою систему учетных данных.</span><span class="sxs-lookup"><span data-stu-id="92062-130">For production purposes, use [ADAL](#authenticate-with-token-credentials) or your own credentials system.</span></span>
> <span data-ttu-id="92062-131">Любые изменения конфигурации CLI повлияют на выполнение пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="92062-131">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="92062-132">Чтобы указать активные учетные данные, используйте команду [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="92062-132">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="92062-133">По умолчанию используется существующий идентификатор подписки, но вы также можете указать его с помощью команды [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="92062-133">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a><span data-ttu-id="92062-134">Проверка подлинности с использованием учетных данных токена (для прежних версий)</span><span class="sxs-lookup"><span data-stu-id="92062-134">Authenticate with token credentials (legacy)</span></span>

<span data-ttu-id="92062-135">В предыдущей версии пакета SDK библиотека ADAL не была доступна, и мы указывали класс `UserPassCredentials`.</span><span class="sxs-lookup"><span data-stu-id="92062-135">In previous version of the SDK, ADAL was not yet available and we provided a `UserPassCredentials` class.</span></span> <span data-ttu-id="92062-136">Такая проверка подлинности считается устаревшей, и мы не рекомендуем ее применять.</span><span class="sxs-lookup"><span data-stu-id="92062-136">This is considered deprecated and should not be used anymore.</span></span>

<span data-ttu-id="92062-137">В примере ниже показан сценарий с использованием имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="92062-137">This sample shows user/password scenario.</span></span> <span data-ttu-id="92062-138">Такой сценарий не поддерживает двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="92062-138">This does not support 2FA.</span></span>

```python
    from azure.common.credentials import UserPassCredentials

    credentials = UserPassCredentials(
        'user@domain.com',
        'my_smart_password'
    )
```
