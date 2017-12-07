---
title: "Проверка подлинности с помощью библиотек управления Azure для Python"
description: "Проверка подлинности с помощью субъекта-службы в библиотеках управления Azure для Python"
keywords: Azure, Python, SDK, API, authentication, active directory, service principal
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/24/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 5c4cf1dee7d9864e809f2797ad49ce78886a6f66
ms.sourcegitcommit: c57305dad01cad925faf50a64953c408429d4ca9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a>Проверка подлинности с помощью библиотек управления Azure для Python

Существует несколько способов проверки подлинности приложения с помощью библиотек управления Azure для Python при создании ресурсов и управления ими.

## <a name="mgmt-auth-token"></a>Проверка подлинности с использованием учетных данных токена

Учетные данные можно безопасно хранить в файле конфигурации, реестре или Azure Key Vault.

В следующем примере для проверки подлинности используется [субъект-служба](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json).

> [!NOTE]
> Вы можете создать субъект-службу с помощью Azure CLI 2.0.
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

> [Примечание.] Чтобы подключиться к одному из независимых облаков Azure, используйте параметр `cloud_environment`.

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

Если требуется более строгий контроль, рекомендуем использовать [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) и программу-оболочку ADAL для SDK. Список всех доступных сценариев и примеры см. на веб-сайте ADAL. Пример проверки подлинности на основе субъекта-службы:

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

Все допустимые вызовы ADAL можно использовать с классом `AdalAuthentication`.

Затем создайте клиентский объект, чтобы приступить к работе с API.

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> [Примечание.] Если используется независимое облако Azure, при создании клиента управления необходимо также указать соответствующий базовый URL-адрес (используя константы в `msrestazure.azure_cloud`). Пример для облака Azure для Китая:
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.active_directory_resource_id)
> ```


## <a name="mgmt-auth-file"></a>Проверка подлинности на основе файлов

Самый простой способ реализовать проверку подлинности — создать JSON-файл, который содержит учетные данные для субъекта-службы Azure. Вы можете одновременно создать субъект-службу и этот файл с помощью следующей команды интерфейса командной строки:

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

Сохраните этот файл в безопасном расположении в вашей системе, доступном для кода. Задайте переменную среды и укажите полный путь к файлу в оболочке:

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

Если вы хотите создать файл самостоятельно, придерживайтесь следующего формата:

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

Затем можно создать любой клиент с помощью фабрики клиента.
```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a>Аутентификация на основе удостоверения управляемой службы (MSI) 
MSI позволяет ресурсу в Azure использовать пакет SDK или CLI без необходимости создать соответствующие учетные данные.

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

## <a name="mgmt-auth-cli"></a>Проверка подлинности на основе интерфейса командной строки

Пакет SDK позволяет создать клиент, используя активную подписку CLI.

> [!IMPORTANT]
> Эти инструкции следует применять в качестве краткого руководства по разработке. В рабочей среде используйте [ADAL](#authenticate-with-token-credentials) или свою систему учетных данных.
> Любые изменения конфигурации CLI повлияют на выполнение пакета SDK.

Чтобы указать активные учетные данные, используйте команду [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).
По умолчанию используется существующий идентификатор подписки, но вы также можете указать его с помощью команды [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a>Проверка подлинности с использованием учетных данных токена (для прежних версий)

В предыдущей версии пакета SDK библиотека ADAL не была доступна, и мы указывали класс `UserPassCredentials`. Такая проверка подлинности считается устаревшей, и мы не рекомендуем ее применять.

В примере ниже показан сценарий с использованием имени пользователя и пароля. Такой сценарий не поддерживает двухфакторную проверку подлинности.

```python
    from azure.common.credentials import UserPassCredentials

    credentials = UserPassCredentials(
        'user@domain.com',
        'my_smart_password',
    )
```
