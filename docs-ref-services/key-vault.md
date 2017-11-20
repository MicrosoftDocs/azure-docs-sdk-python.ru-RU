---
title: "Библиотеки Azure Key Vault для Python"
description: "Справочная документация по клиентским библиотекам Azure Key Vault для Python"
author: lisawong19
keywords: Azure, Python, SDK, API, Keys, Key Vault, Authentication, Secret, key, security
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 3eac46eb4d5d19273ead9f19b739f6fb6d72e5cc
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="23fb1-104">Библиотеки Azure Key Vault для Python</span><span class="sxs-lookup"><span data-stu-id="23fb1-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="23fb1-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="23fb1-105">Overview</span></span>

<span data-ttu-id="23fb1-106">Создавайте, обновляйте и удаляйте ключи и секреты в Azure Key Vault с помощью клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="23fb1-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="23fb1-107">Используйте библиотеки управления Azure Key Vault, чтобы создавать хранилища ключей, авторизовать приложения и управлять разрешениями.</span><span class="sxs-lookup"><span data-stu-id="23fb1-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="23fb1-108">Подробнее об [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="23fb1-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="23fb1-109">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="23fb1-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="23fb1-110">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="23fb1-110">Client library</span></span>
```bash
pip install azure-keyvault
```

## <a name="example"></a><span data-ttu-id="23fb1-111">Пример</span><span class="sxs-lookup"><span data-stu-id="23fb1-111">Example</span></span>
<span data-ttu-id="23fb1-112">Получите [веб-ключ JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) из Key Vault.</span><span class="sxs-lookup"><span data-stu-id="23fb1-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callack(server, resource, scope):
    credentials = credentials or ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = resource
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callack))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```
[!div class="nextstepaction"]
[<span data-ttu-id="23fb1-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="23fb1-113">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/clientlibrary)

### <a name="management-api"></a><span data-ttu-id="23fb1-114">API управления</span><span class="sxs-lookup"><span data-stu-id="23fb1-114">Management API</span></span>
```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="23fb1-115">Пример</span><span class="sxs-lookup"><span data-stu-id="23fb1-115">Example</span></span>
<span data-ttu-id="23fb1-116">В следующем примере показано, как создать Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="23fb1-116">The following example shows how to create an Azure Key Vault.</span></span> 

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
> [<span data-ttu-id="23fb1-117">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="23fb1-117">Explore the Management APIs</span></span>](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [<span data-ttu-id="23fb1-118">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="23fb1-118">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/managementlibrary)

## <a name="samples"></a><span data-ttu-id="23fb1-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="23fb1-119">Samples</span></span>
* <span data-ttu-id="23fb1-120">[Управление хранилищами ключей][1]</span><span class="sxs-lookup"><span data-stu-id="23fb1-120">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="23fb1-121">[Восстановление Key Vault][2]</span><span class="sxs-lookup"><span data-stu-id="23fb1-121">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="23fb1-122">Просмотрите [полный список](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) примеров для Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="23fb1-122">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 