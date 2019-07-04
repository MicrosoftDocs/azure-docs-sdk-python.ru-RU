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
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="92e25-103">Библиотеки Azure Key Vault для Python</span><span class="sxs-lookup"><span data-stu-id="92e25-103">Azure Key Vault libraries for Python</span></span>

<span data-ttu-id="92e25-104">[Azure Key Vault](/azure/key-vault/) — это система Azure для хранения криптографических ключей, секретов и сертификатов, а также управления ими.</span><span class="sxs-lookup"><span data-stu-id="92e25-104">[Azure Key Vault](/azure/key-vault/) is Azure's storage and management system for cryptographic keys, secrets, and certificate management.</span></span> <span data-ttu-id="92e25-105">API пакета SDK Python для Key Vault реализован в виде клиентских библиотек и библиотек управления.</span><span class="sxs-lookup"><span data-stu-id="92e25-105">The Python SDK API for Key Vault is split between client libraries and management libraries.</span></span>

<span data-ttu-id="92e25-106">Используйте клиентские библиотеки, чтобы:</span><span class="sxs-lookup"><span data-stu-id="92e25-106">Use the client library to:</span></span>
- <span data-ttu-id="92e25-107">обновлять, удалять элементы Azure Key Vault или получать к ним доступ;</span><span class="sxs-lookup"><span data-stu-id="92e25-107">Access, update, or delete items stored in an Azure Key Vault</span></span>
- <span data-ttu-id="92e25-108">получать метаданные для сохраненных сертификатов;</span><span class="sxs-lookup"><span data-stu-id="92e25-108">Get metadata for stored certificates</span></span>
- <span data-ttu-id="92e25-109">проверять подписи на соответствие симметричным ключам в Key Vault.</span><span class="sxs-lookup"><span data-stu-id="92e25-109">Verify signatures against symmetric keys in Key Vault</span></span>

<span data-ttu-id="92e25-110">Используйте библиотеки управления, чтобы:</span><span class="sxs-lookup"><span data-stu-id="92e25-110">Use the management library to:</span></span>
- <span data-ttu-id="92e25-111">создавать, обновлять или удалять новые хранилища Key Vault;</span><span class="sxs-lookup"><span data-stu-id="92e25-111">Create, update, or delete new Key Vault stores</span></span>
- <span data-ttu-id="92e25-112">управлять политиками доступа к хранилищу;</span><span class="sxs-lookup"><span data-stu-id="92e25-112">Control vault access policies</span></span>
- <span data-ttu-id="92e25-113">выводить список хранилищ по подписке или группе ресурсов;</span><span class="sxs-lookup"><span data-stu-id="92e25-113">List vaults by subscription or resource group</span></span>
- <span data-ttu-id="92e25-114">проверять, свободно ли имя для хранилища.</span><span class="sxs-lookup"><span data-stu-id="92e25-114">Check for vault name availability</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="92e25-115">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="92e25-115">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="92e25-116">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="92e25-116">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="92e25-117">Примеры</span><span class="sxs-lookup"><span data-stu-id="92e25-117">Examples</span></span>

<span data-ttu-id="92e25-118">В примерах ниже используется аутентификация с помощью субъекта-службы, которая является рекомендуемым способом входа для подключающихся к Azure приложений.</span><span class="sxs-lookup"><span data-stu-id="92e25-118">The following examples use service principal authentication, which is the recommended sign in method for applications that connect to Azure.</span></span> <span data-ttu-id="92e25-119">Подробные сведения об аутентификации с помощью субъекта-службы см. в статье [Проверка подлинности с помощью библиотек управления Azure для Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="92e25-119">To learn about service principal authentication, see [Authenticate with the Azure SDK for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span></span>

<span data-ttu-id="92e25-120">Извлеките открытую часть ассиметричного ключа из хранилища:</span><span class="sxs-lookup"><span data-stu-id="92e25-120">Retrieve the public portion of an asymmetric key from a vault:</span></span>

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

<span data-ttu-id="92e25-121">Извлеките секрет из хранилища:</span><span class="sxs-lookup"><span data-stu-id="92e25-121">Retrieve a secret from a vault:</span></span>

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
> [<span data-ttu-id="92e25-122">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="92e25-122">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a><span data-ttu-id="92e25-123">Библиотека управления</span><span class="sxs-lookup"><span data-stu-id="92e25-123">Management library</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="92e25-124">Пример</span><span class="sxs-lookup"><span data-stu-id="92e25-124">Example</span></span>

<span data-ttu-id="92e25-125">В следующем примере показано, как создать Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="92e25-125">The following example shows how to create an Azure Key Vault.</span></span> 

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
> [<span data-ttu-id="92e25-126">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="92e25-126">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="92e25-127">Примеры</span><span class="sxs-lookup"><span data-stu-id="92e25-127">Samples</span></span>
* <span data-ttu-id="92e25-128">[Управление хранилищами Azure Key Vault][1]</span><span class="sxs-lookup"><span data-stu-id="92e25-128">[Manage Azure Key Vaults][1]</span></span> 
* <span data-ttu-id="92e25-129">[Восстановление Azure Key Vault][2]</span><span class="sxs-lookup"><span data-stu-id="92e25-129">[Azure Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="92e25-130">Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) примеров для Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="92e25-130">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
