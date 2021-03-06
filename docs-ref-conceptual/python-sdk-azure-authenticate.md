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
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a>Проверка подлинности с помощью библиотек управления Azure для Python

Существует несколько способов проверки подлинности приложения с помощью библиотек управления Azure для Python при создании ресурсов и управления ими.

## <a name="mgmt-auth-token"></a>Проверка подлинности с использованием учетных данных токена

Учетные данные можно безопасно хранить в файле конфигурации, реестре или Azure Key Vault.

В следующем примере для проверки подлинности используется [субъект-служба](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json).

> [!NOTE]
> Чтобы создать субъект-службу с помощью Azure CLI, используйте следующую команду:
>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```
>
> См. подробнее о [создании и настройке субъекта-службы Azure с помощью Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli).

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

> [Примечание.] Чтобы подключиться к одному из независимых облаков Azure, используйте параметр `cloud_environment`.
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
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
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

Затем можно создать любой клиент с помощью фабрики клиента.

```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a>Аутентификация с помощью управляемых удостоверений Azure
Управляемые удостоверения Azure позволяют использовать пакеты SDK или CLI для ресурсов в Azure без необходимости создавать соответствующие учетные данные.

> [!IMPORTANT]
>
> Для использования управляемых удостоверений нужно подключиться к Azure из ресурсов Azure, таких как функция Azure или виртуальная машина, работающая в Azure. См. подробнее об управляемых удостоверениях для ресурсов Azure в руководствах по [настройке](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) и [использованию управляемых удостоверений для ресурсов Azure](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).

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

Пакет SDK позволяет создать клиент, используя активную подписку Azure CLI.

> [!IMPORTANT]
> Эти инструкции следует применять в качестве краткого руководства по разработке. В рабочей среде используйте [ADAL](#mgmt-auth-legacy) или свою систему учетных данных.
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
    'my_smart_password'
)
```
