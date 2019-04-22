---
title: Пакет SDK Azure HDInsight для Python
description: Справочник по пакету SDK Azure HDInsight для Python. Пакет SDK HDInsight для Python предоставляет классы и методы для управления кластерами HDInsight.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 04/10/2019
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: ea9599be9fead5f964fbd4ce4e4bdc78a445918c
ms.sourcegitcommit: 375a1f9180eb1323fe2af0a7e28fd4676973c68e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/16/2019
ms.locfileid: "59586822"
---
# <a name="hdinsight-sdk-for-python"></a>Пакет SDK HDInsight для Python

## <a name="overview"></a>Обзор

Пакет SDK HDInsight для Python предоставляет классы и методы для управления кластерами HDInsight. Пакет также поддерживает операции создания, удаления, обновления, получения списков, масштабирования, выполнения скриптов, мониторинга, получения свойства кластеров HDInsight и т. д.

## <a name="prerequisites"></a>Предварительные требования

* Учетная запись Azure. Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).
* [Python](https://www.python.org/downloads/)
* [pip](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a>Установка пакета SDK

Пакет SDK HDInsight для Python можно найти на сайте [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) и установить с помощью команды: 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a>Authentication

Для использования пакета SDK нужно выполнить аутентификацию с помощью подписки Azure.  Ниже описано, как создать субъект-службу и использовать его для аутентификации. После этого вы получите экземпляр `HDInsightManagementClient`, в котором доступны различные методы (описанные далее) для операций управления.

> [!NOTE]
> Кроме описанного выше, есть и другие методы аутентификации, которые могут оказаться удобнее для вас. Все способы описаны в статье [Проверка подлинности с помощью библиотек управления Azure для Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)

### <a name="authentication-example-using-a-service-principal"></a>Пример аутентификации с помощью субъекта-службы

Сначала войдите в [Azure Cloud Shell](https://shell.azure.com/bash). Убедитесь, что вы используете подписку, в которой будет создан субъект-служба. 

```azurecli-interactive
az account show
```

Сведения о подписке отображаются в формате JSON.

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

Если вы вошли не в ту подписку, выполните такую команду, чтобы выбрать правильную подписку: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Если вы еще не зарегистрировали поставщик ресурсов HDInsight с помощью другого метода (например, создав кластер HDInsight на портале Azure), вам необходимо это сделать, прежде чем выполнять аутентификацию. Это можно сделать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Создайте субъект-службу, выбрав имя и выполнив такую команду:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Сведения о субъекте-службе отображаются в виде JSON.

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
Скопируйте фрагмент кода Python ниже и задайте в качестве значений `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` и `SUBSCRIPTION_ID` строки из JSON-файла, возвращенного после выполнения команды для создания субъекта-службы.

```python
from azure.mgmt.hdinsight import HDInsightManagementClient
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.hdinsight.models import *

# Tenant ID for your Azure Subscription
TENANT_ID = ''
# Your Service Principal App Client ID
CLIENT_ID = ''
# Your Service Principal Client Secret
CLIENT_SECRET = ''
# Your Azure Subscription ID
SUBSCRIPTION_ID = ''

credentials = ServicePrincipalCredentials(
    client_id = CLIENT_ID,
    secret = CLIENT_SECRET,
    tenant = TENANT_ID
)

client = HDInsightManagementClient(credentials, SUBSCRIPTION_ID)
```


## <a name="cluster-management"></a>Управление кластерами

> [!NOTE]
> В этом разделе предполагается, что вы уже выполнили аутентификацию, создали экземпляр `HDInsightManagementClient` и сохранили его в переменной с именем `client`. Инструкции по выполнению аутентификации и получению `HDInsightManagementClient` см. в предыдущем разделе.

### <a name="create-a-cluster"></a>Создание кластера

Кластер можно создать, вызвав `client.clusters.create()`.

#### <a name="samples"></a>Примеры

Для создания нескольких распространенных типов кластеров HDInsight доступны примеры кода: [доступны примеры кода Python](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).

#### <a name="example"></a>Пример

В этом примере показано, как создать кластер Spark с двумя головными узлами и одним рабочим.

> [!NOTE]
> Сначала необходимо создать группу ресурсов и учетную запись хранения, как описано далее. Если они уже созданы, следующие шаги можно пропустить.

##### <a name="creating-a-resource-group"></a>Создание группы ресурсов

Группу ресурсов можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Создание учетной записи хранения

Учетную запись хранения можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Теперь выполните такую команду, чтобы получить ключ для учетной записи хранения (он потребуется для создания кластера):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
Показанный ниже фрагмент кода Python создает кластер Spark с двумя головными узлами и одним рабочим. Задайте переменные, как описано в комментариях, и при необходимости измените другие параметры.

```python
# The name for the cluster you are creating
cluster_name = ""
# The name of your existing Resource Group
resource_group_name = ""
# Choose a username
username = ""
# Choose a password
password = ""
# Replace <> with the name of your storage account
storage_account = "<>.blob.core.windows.net"
# Storage account key you obtained above
storage_account_key = ""
# Choose a region
location = ""
container = "default"

params = ClusterCreateProperties(
    cluster_version="3.6",
    os_type=OSType.linux,
    tier=Tier.standard,
    cluster_definition=ClusterDefinition(
        kind="spark",
        configurations={
            "gateway": {
                "restAuthCredential.enabled_credential": "True",
                "restAuthCredential.username": username,
                "restAuthCredential.password": password
            }
        }
    ),
    compute_profile=ComputeProfile(
        roles=[
            Role(
                name="headnode",
                target_instance_count=2,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            ),
            Role(
                name="workernode",
                target_instance_count=1,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            )
        ]
    ),
    storage_profile=StorageProfile(
        storageaccounts=[StorageAccount(
            name=storage_account,
            key=storage_account_key,
            container=container,
            is_default=True
        )]
    )
)

client.clusters.create(
    cluster_name=cluster_name,
    resource_group_name=resource_group_name,
    parameters=ClusterCreateParametersExtended(
        location=location,
        tags={},
        properties=params
    ))
```

### <a name="get-cluster-details"></a>Получение сведений о кластере

Чтобы получить сведения о свойствах кластера, выполните такую команду:

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Пример

Чтобы убедиться в том, что вы создали кластер, можно использовать `get`.

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

Выходные данные должны выглядеть так:

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a>Получение списка кластеров

#### <a name="list-clusters-under-the-subscription"></a>Получение списка кластеров в пределах подписки

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a>Получение списка кластеров в пределах в группы ресурсов

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> Вызов `list()` и `list_by_resource_group()` возвращает объект `ClusterPaged`. Вызов `advance_page()` возвращает список кластеров на этой странице и перемещает объект `ClusterPaged` на следующую страницу. Этот вызов можно повторять до тех пор, пока не будет получено исключение `StopIteration`, означающее отсутствие дальнейших страниц.

#### <a name="example"></a>Пример

В следующем примере выводятся свойства всех кластеров в пределах текущей подписки:

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a>Удаление кластера

Чтобы удалить кластер, выполните такую команду:

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a>Обновление тегов кластера

Вы можете обновить теги кластера так:

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a>Пример

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a>Изменение размера кластера

Вы можете изменить размер кластера, изменяя количество его рабочих узлов. Укажите новый размер, как показано ниже:

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a>Мониторинг кластера

Пакет Azure Management SDK для HDInsight также позволяет управлять мониторингом кластеров с помощью Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Включение мониторинга OMS

> [!NOTE]
> Чтобы включить мониторинг OMS, требуется рабочая область Log Analytics. Если вы не создавали такую рабочую область, см. статью [Создание рабочей области Log Analytics на портале Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Чтобы включить мониторинг OMS в кластере, выполните такую команду:

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a>Просмотр состояния мониторинга OMS

Чтобы узнать состояние мониторинга OMS в кластере, выполните такую команду:

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a>Отключение мониторинга OMS

Чтобы отключить мониторинг OMS в кластере, выполните такую команду:

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a>Элемент "Действия скрипта"

В кластерах HDInsight поддерживается метод конфигурации с использованием, действий скриптов, который вызывает пользовательские скрипты для настройки кластера.
> [!NOTE]
> Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действий сценариев](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

### <a name="execute-script-actions"></a>Выполнение действий скриптов
Для выполнения действий скриптов в указанном кластере:

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Удаление действий скриптов

Чтобы удалить сохраненные действия скриптов в кластере, выполните такую команду:

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a>Получение списка сохраненных действий скриптов

> [!NOTE]
> Методы `list()` и `list_persisted_scripts()` возвращают объект `RuntimeScriptActionDetailPaged`. Вызов `advance_page()` возвращает список объектов `RuntimeScriptActionDetail` на соответствующей странице и перемещает объект `RuntimeScriptActionDetailPaged` на следующую страницу. Этот вызов можно повторять до тех пор, пока не будет получено исключение `StopIteration`, означающее отсутствие дальнейших страниц. См. пример ниже.

Чтобы получить список всех сохраненных действий скриптов в кластере, выполните такую команду:
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Пример

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a>Просмотр журнала выполнения всех скриптов

Чтобы получить журнал выполнения всех скриптов в кластере, выполните такую команду:

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Пример

В этом примере выводятся сведения обо всех выполнявшихся скриптах.

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
