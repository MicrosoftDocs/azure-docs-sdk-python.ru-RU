---
title: Проверка подлинности с помощью библиотек управления Azure для Python
description: Проверка подлинности с помощью субъекта-службы в библиотеках управления Azure для Python
keywords: Azure, Python, SDK, API, authentication, active directory, service principal
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 04/11/2019
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 51f26b120cefffd2d7f4af9c2b6b2cb532bc6006
ms.sourcegitcommit: 375a1f9180eb1323fe2af0a7e28fd4676973c68e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2019
ms.locfileid: "59586812"
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a><span data-ttu-id="561cc-104">Проверка подлинности с помощью библиотек управления Azure для Python</span><span class="sxs-lookup"><span data-stu-id="561cc-104">Authenticate with the Azure Management Libraries for Python</span></span>

<span data-ttu-id="561cc-105">Существует несколько способов проверки подлинности приложения с помощью библиотек управления Azure для Python при создании ресурсов и управления ими.</span><span class="sxs-lookup"><span data-stu-id="561cc-105">Several options are available to authenticate your application with Azure when using the Python management libraries to create and manage resources.</span></span>

## <a name="mgmt-auth-token"></a><span data-ttu-id="561cc-106">Проверка подлинности с использованием учетных данных токена</span><span class="sxs-lookup"><span data-stu-id="561cc-106">Authenticate with token credentials</span></span>

<span data-ttu-id="561cc-107">Учетные данные можно безопасно хранить в файле конфигурации, реестре или Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="561cc-107">Store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

<span data-ttu-id="561cc-108">В следующем примере для проверки подлинности используется [субъект-служба](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="561cc-108">The following example uses a [Service Principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) for authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="561cc-109">Чтобы создать субъект-службу с помощью Azure CLI, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="561cc-109">To create a service principal with the Azure CLI, use the following command:</span></span>
>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```
>
> <span data-ttu-id="561cc-110">См. подробнее о [создании и настройке субъекта-службы Azure с помощью Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="561cc-110">To learn more about setting up service princpals with the CLI, see [Create an Azure service principal with Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

```python
from azure.common.credentials import ServicePrincipalCredentials

# Tenant ID for your Azure subscription
TENANT_ID = '<Your tenant ID>'

# Your service principal App ID
CLIENT = '<Your service principal ID>'

# Your service principal password
KEY = '<Your service principal password>'

credentials = ServicePrincipalCredentials(
    client_id = CLIENT,
    secret = KEY,
    tenant = TENANT_ID
)
```

> <span data-ttu-id="561cc-111">[Примечание.] Чтобы подключиться к одному из независимых облаков Azure, используйте параметр `cloud_environment`.</span><span class="sxs-lookup"><span data-stu-id="561cc-111">[NOTE!] To connect to one of the Azure sovereign clouds, use the `cloud_environment` parameter.</span></span>
>
> ```python
> from azure.common.credentials import ServicePrincipalCredentials
> from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
> 
> # Tenant ID for your Azure Subscription
> TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
> 
> # Your Service Principal App ID
> CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'
> 
> # Your Service Principal Password
> KEY = 'password'
> 
> credentials = ServicePrincipalCredentials(
>     client_id = CLIENT,
>     secret = KEY,
>     tenant = TENANT_ID,
>     cloud_environment = AZURE_CHINA_CLOUD
> )
> ```

<span data-ttu-id="561cc-112">Если требуется более строгий контроль, рекомендуем использовать [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) и программу-оболочку ADAL для SDK.</span><span class="sxs-lookup"><span data-stu-id="561cc-112">If you need more control, it is recommended to use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) and the SDK ADAL wrapper.</span></span> <span data-ttu-id="561cc-113">Список всех доступных сценариев и примеры см. на веб-сайте ADAL.</span><span class="sxs-lookup"><span data-stu-id="561cc-113">Please refer to the ADAL website for all the available scenarios list and samples.</span></span> <span data-ttu-id="561cc-114">Пример проверки подлинности на основе субъекта-службы:</span><span class="sxs-lookup"><span data-stu-id="561cc-114">For instance for service principal authentication:</span></span>

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

<span data-ttu-id="561cc-115">Все допустимые вызовы ADAL можно использовать с классом `AdalAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="561cc-115">All ADAL valid calls can be used with the `AdalAuthentication` class.</span></span>

<span data-ttu-id="561cc-116">Затем создайте клиентский объект, чтобы приступить к работе с API.</span><span class="sxs-lookup"><span data-stu-id="561cc-116">Next, create a client object to start working with the API:</span></span>

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> <span data-ttu-id="561cc-117">[Примечание.] Если используется независимое облако Azure, при создании клиента управления необходимо также указать соответствующий базовый URL-адрес (используя константы в `msrestazure.azure_cloud`).</span><span class="sxs-lookup"><span data-stu-id="561cc-117">[NOTE!] When using an Azure sovereign cloud you must also specify the appropriate base URL (via the constants in `msrestazure.azure_cloud`) when creating the management client.</span></span> <span data-ttu-id="561cc-118">Пример для облака Azure для Китая:</span><span class="sxs-lookup"><span data-stu-id="561cc-118">For example for Azure China Cloud:</span></span>
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
> ```


## <a name="mgmt-auth-file"></a><span data-ttu-id="561cc-119">Проверка подлинности на основе файлов</span><span class="sxs-lookup"><span data-stu-id="561cc-119">File based authentication</span></span>

<span data-ttu-id="561cc-120">Самый простой способ реализовать проверку подлинности — создать JSON-файл, который содержит учетные данные для субъекта-службы Azure.</span><span class="sxs-lookup"><span data-stu-id="561cc-120">The simplest way to authenticate is to create a JSON file that contains credentials for an Azure Service Principal.</span></span> <span data-ttu-id="561cc-121">Вы можете одновременно создать субъект-службу и этот файл с помощью следующей команды интерфейса командной строки:</span><span class="sxs-lookup"><span data-stu-id="561cc-121">You can use the following CLI command to create a new Service Principal and this file at the same time:</span></span>

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

<span data-ttu-id="561cc-122">Сохраните этот файл в безопасном расположении в вашей системе, доступном для кода.</span><span class="sxs-lookup"><span data-stu-id="561cc-122">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="561cc-123">Задайте переменную среды и укажите полный путь к файлу в оболочке:</span><span class="sxs-lookup"><span data-stu-id="561cc-123">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

<span data-ttu-id="561cc-124">Если вы хотите создать файл самостоятельно, придерживайтесь следующего формата:</span><span class="sxs-lookup"><span data-stu-id="561cc-124">If you want to create the file yourself, please follow this format:</span></span>

```json
{
    "clientId": "<Service principal ID>",
    "clientSecret": "<Service principal secret/password>",
    "subscriptionId": "<Subscription associated with the service principal>",
    "tenantId": "<The service principal's tenant>",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="561cc-125">Затем можно создать любой клиент с помощью фабрики клиента.</span><span class="sxs-lookup"><span data-stu-id="561cc-125">You can then create any client using the client factory:</span></span>

```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a><span data-ttu-id="561cc-126">Аутентификация с помощью управляемых удостоверений Azure</span><span class="sxs-lookup"><span data-stu-id="561cc-126">Authenticate with Azure Managed Identities</span></span>
<span data-ttu-id="561cc-127">Управляемые удостоверения Azure позволяют использовать пакеты SDK или CLI для ресурсов в Azure без необходимости создавать соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="561cc-127">Azure Managed Identity is a simple way for a resource in Azure to use SDK/CLI without the need to create specific credentials.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="561cc-128">Для использования управляемых удостоверений нужно подключиться к Azure из ресурсов Azure, таких как функция Azure или виртуальная машина, работающая в Azure.</span><span class="sxs-lookup"><span data-stu-id="561cc-128">To use managed identities, you must be connecting to Azure from an Azure resource, such as an Azure Function or a VM running in Azure.</span></span> <span data-ttu-id="561cc-129">См. подробнее об управляемых удостоверениях для ресурсов Azure в руководствах по [настройке](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) и [использованию управляемых удостоверений для ресурсов Azure](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).</span><span class="sxs-lookup"><span data-stu-id="561cc-129">To learn how to configure a managed identity for a resource, see [Configure managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) and [How to use managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).</span></span>

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

## <a name="mgmt-auth-cli"></a><span data-ttu-id="561cc-130">Проверка подлинности на основе интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="561cc-130">CLI-based authentication</span></span>

<span data-ttu-id="561cc-131">Пакет SDK позволяет создать клиент, используя активную подписку Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="561cc-131">The SDK is able to create a client using the Azure CLI's active subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="561cc-132">Эти инструкции следует применять в качестве краткого руководства по разработке.</span><span class="sxs-lookup"><span data-stu-id="561cc-132">This should be used as quick start developer experience.</span></span> <span data-ttu-id="561cc-133">В рабочей среде используйте [ADAL](#mgmt-auth-legacy) или свою систему учетных данных.</span><span class="sxs-lookup"><span data-stu-id="561cc-133">For production purposes, use [ADAL](#mgmt-auth-legacy) or your own credentials system.</span></span>
> <span data-ttu-id="561cc-134">Любые изменения конфигурации CLI повлияют на выполнение пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="561cc-134">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="561cc-135">Чтобы указать активные учетные данные, используйте команду [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="561cc-135">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="561cc-136">По умолчанию используется существующий идентификатор подписки, но вы также можете указать его с помощью команды [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="561cc-136">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a><span data-ttu-id="561cc-137">Проверка подлинности с использованием учетных данных токена (для прежних версий)</span><span class="sxs-lookup"><span data-stu-id="561cc-137">Authenticate with token credentials (legacy)</span></span>

<span data-ttu-id="561cc-138">В предыдущей версии пакета SDK библиотека ADAL не была доступна, и мы указывали класс `UserPassCredentials`.</span><span class="sxs-lookup"><span data-stu-id="561cc-138">In previous version of the SDK, ADAL was not yet available and we provided a `UserPassCredentials` class.</span></span> <span data-ttu-id="561cc-139">Такая проверка подлинности считается устаревшей, и мы не рекомендуем ее применять.</span><span class="sxs-lookup"><span data-stu-id="561cc-139">This is considered deprecated and should not be used anymore.</span></span>

<span data-ttu-id="561cc-140">В примере ниже показан сценарий с использованием имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="561cc-140">This sample shows user/password scenario.</span></span> <span data-ttu-id="561cc-141">Такой сценарий не поддерживает двухфакторную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="561cc-141">This does not support 2FA.</span></span>

```python
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
    'user@domain.com',
    'my_smart_password'
)
```
