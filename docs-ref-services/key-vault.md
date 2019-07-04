---
title: Библиотеки Azure Key Vault для Python
description: Справочная документация по клиентским библиотекам Azure Key Vault для Python
author: sptramer
manager: carmonm
ms.author: sttramer
ms.date: 06/10/2019
ms.topic: conceptual
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: f4661ee389c13ce8546e7b5cc8866ab7b216d3b0
ms.sourcegitcommit: 92fa5dbcfd9a20f4a49da5f4bdc03045783d3495
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2019
ms.locfileid: "67149329"
---
# <a name="azure-key-vault-libraries-for-python"></a>Библиотеки Azure Key Vault для Python

[Azure Key Vault](/azure/key-vault/) — это система Azure для хранения криптографических ключей, секретов и сертификатов, а также управления ими. API пакета SDK Python для Key Vault реализован в виде клиентских библиотек и библиотек управления.

Используйте клиентские библиотеки, чтобы:
- обновлять, удалять элементы Azure Key Vault или получать к ним доступ;
- получать метаданные для сохраненных сертификатов;
- проверять подписи на соответствие симметричным ключам в Key Vault.

Используйте библиотеки управления, чтобы:
- создавать, обновлять или удалять новые хранилища Key Vault;
- управлять политиками доступа к хранилищу;
- выводить список хранилищ по подписке или группе ресурсов;
- проверять, свободно ли имя для хранилища.

## <a name="install-the-libraries"></a>Установка библиотек

### <a name="client-library"></a>Клиентская библиотека

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Примеры

В примерах ниже используется аутентификация с помощью субъекта-службы, которая является рекомендуемым способом входа для подключающихся к Azure приложений. Подробные сведения об аутентификации с помощью субъекта-службы см. в статье [Проверка подлинности с помощью библиотек управления Azure для Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate).

Извлеките открытую часть ассиметричного ключа из хранилища:

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# KEY_VERSION is required, and can be obtained with the KeyVaultClient.get_key_versions(self, vault_url, key_name) API
key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
key = key_bundle.key
```

Извлеките секрет из хранилища:

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# SECRET_VERSION is required, and can be obtained with the KeyVaultClient.get_secret_versions(self, vault_url, secret_id) API
secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)
secret = secret_bundle.value
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a>Библиотека управления

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Пример

В следующем примере показано, как создать Azure Key Vault. 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient
from azure.common.credentials import ServicePrincipalCredentials


credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

# Even when using service principal credentials, a subscription ID is required. For service principals,
# this should be the subscription used to create the service principal. Storing a token like a valid
# subscription ID in code is not recommended and only shown here for example purposes.
SUBSCRIPTION_ID = '...'
client = KeyVaultManagementClient(credentials, SUBSCRIPTION_ID)

# The object ID and organization ID (tenant) of the user, application, or service principal for access policies.
# These values can be found through the Azure CLI or the Portal.
ALLOW_OBJECT_ID = '...'
ALLOW_TENANT_ID = '...'

RESOURCE_GROUP = '...'
VAULT_NAME = '...'

# Vault properties may also be created by using the azure.mgmt.keyvault.models.VaultCreateOrUpdateParameters
# class, rather than a map. 
operation = client.vaults.create_or_update(
    RESOURCE_GROUP,
    VAULT_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'object_id': OBJECT_ID,
                'tenant_id': ALLOW_TENANT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()
print(f'New vault URI: {vault.properties.vault_uri}')
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Примеры
* [Управление хранилищами Azure Key Vault][1] 
* [Восстановление Azure Key Vault][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) примеров для Azure Key Vault. 
