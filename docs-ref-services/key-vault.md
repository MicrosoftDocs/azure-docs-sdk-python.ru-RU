---
title: Библиотеки Azure Key Vault для Python
description: Справочная документация по клиентским библиотекам Azure Key Vault для Python
author: lisawong19
keywords: Azure, Python, SDK, API, Keys, Key Vault, Authentication, Secret, key, security
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 3e7d9970f5799708c6822493106aec5466de52d9
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/18/2018
ms.locfileid: "35719645"
---
# <a name="azure-key-vault-libraries-for-python"></a>Библиотеки Azure Key Vault для Python

## <a name="overview"></a>Обзор

Создавайте, обновляйте и удаляйте ключи и секреты в Azure Key Vault с помощью клиентских библиотек.

Используйте библиотеки управления Azure Key Vault, чтобы создавать хранилища ключей, авторизовать приложения и управлять разрешениями. 

Подробнее об [Azure Key Vault](/azure/key-vault/key-vault-whatis).

## <a name="install-the-libraries"></a>Установка библиотек

### <a name="client-library"></a>Клиентская библиотека

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Примеры

Получите [веб-ключ JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) из Key Vault.

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```

Аналогичным образом можно использовать следующий фрагмент кода, чтобы извлечь секрет из хранилища:

```
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

secret_bundle = client.get_secret("https://VAULT_ID.vault.azure.net/", "SECRET_ID", "SECRET_VERSION")

print(secret_bundle.value)
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a>API управления

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Пример
В следующем примере показано, как создать Azure Key Vault. 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient

GROUP_NAME = 'your_resource_group_name'
KV_NAME = 'your_key_vault_name'
#The object ID of the User or Application for access policies. Find this number in the portal
OBJECT_ID = '00000000-0000-0000-0000-000000000000'

kv_client = KeyVaultManagementClient(credentials, subscription_id)

vault = kv_client.vaults.create_or_update(
    GROUP_NAME,
    KV_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': os.environ['AZURE_TENANT_ID'],
            'access_policies': [{
                'tenant_id': os.environ['AZURE_TENANT_ID'],
                'object_id': OBJECT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)
```
> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Примеры
* [Управление хранилищами ключей][1] 
* [Восстановление Key Vault][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) примеров для Azure Key Vault. 
