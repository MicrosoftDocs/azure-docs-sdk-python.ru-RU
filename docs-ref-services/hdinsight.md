---
title: Предварительная версия пакета SDK Azure HDInsight для Python
description: Справочник по пакету SDK Azure HDInsight для Python. Пакет SDK HDInsight для Python предоставляет классы и методы для управления кластерами HDInsight.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 09/18/2018
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 42e1e36b5854fda93188564be3ed3064b9ba4435
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277478"
---
# <a name="hdinsight-python-management-sdk-preview"></a><span data-ttu-id="e73a7-104">Предварительная версия пакета SDK для управления HDInsight с использованием Python</span><span class="sxs-lookup"><span data-stu-id="e73a7-104">HDInsight Python Management SDK Preview</span></span>

## <a name="overview"></a><span data-ttu-id="e73a7-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="e73a7-105">Overview</span></span>

<span data-ttu-id="e73a7-106">Пакет SDK HDInsight для Python предоставляет классы и методы для управления кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e73a7-106">The HDInsight Python SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="e73a7-107">Пакет также поддерживает операции создания, удаления, обновления, получения списков, масштабирования, выполнения скриптов, мониторинга, получения свойства кластеров HDInsight и др.</span><span class="sxs-lookup"><span data-stu-id="e73a7-107">It includes operations to create, delete, update, list, scale, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e73a7-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e73a7-108">Prerequisites</span></span>

* <span data-ttu-id="e73a7-109">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e73a7-109">An Azure account.</span></span> <span data-ttu-id="e73a7-110">Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e73a7-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="e73a7-111">Python</span><span class="sxs-lookup"><span data-stu-id="e73a7-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="e73a7-112">pip</span><span class="sxs-lookup"><span data-stu-id="e73a7-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="e73a7-113">Установка пакета SDK</span><span class="sxs-lookup"><span data-stu-id="e73a7-113">SDK Installation</span></span>

<span data-ttu-id="e73a7-114">Пакет SDK HDInsight для Python можно найти на сайте [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) и установить с помощью команды:</span><span class="sxs-lookup"><span data-stu-id="e73a7-114">The HDInsight Python SDK can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="e73a7-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="e73a7-115">Authentication</span></span>

<span data-ttu-id="e73a7-116">Для использования пакета SDK нужно выполнить аутентификацию с помощью подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="e73a7-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="e73a7-117">Ниже описано, как создать субъект-службу и использовать его для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="e73a7-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="e73a7-118">После этого вы получите экземпляр `HDInsightManagementClient`, в котором доступны различные методы (описанные далее) для операций управления.</span><span class="sxs-lookup"><span data-stu-id="e73a7-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="e73a7-119">Кроме описанного выше, есть и другие методы аутентификации, которые могут оказаться удобнее для вас.</span><span class="sxs-lookup"><span data-stu-id="e73a7-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="e73a7-120">Все методы аутентификации см. в руководстве по [аутентификации с использованием библиотек управления Azure для Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="e73a7-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="e73a7-121">Пример аутентификации с помощью субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="e73a7-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="e73a7-122">Сначала войдите в [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="e73a7-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="e73a7-123">Убедитесь, что вы используете подписку, в которой будет создан субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="e73a7-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="e73a7-124">Сведения о подписке отображаются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e73a7-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="e73a7-125">Если вы вошли не в ту подписку, выполните такую команду, чтобы выбрать правильную подписку:</span><span class="sxs-lookup"><span data-stu-id="e73a7-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="e73a7-126">Если вы еще не зарегистрировали поставщик ресурсов HDInsight с помощью другого метода (например, создав кластер HDInsight на портале Azure), вам необходимо это сделать, прежде чем выполнять аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="e73a7-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="e73a7-127">Это можно сделать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="e73a7-128">Создайте субъект-службу, выбрав имя и выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="e73a7-129">Сведения о субъекте-службе отображаются в виде JSON.</span><span class="sxs-lookup"><span data-stu-id="e73a7-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="e73a7-130">Скопируйте фрагмент кода Python ниже и задайте в качестве значений `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` и `SUBSCRIPTION_ID` строки из JSON-файла, возвращенного после выполнения команды для создания субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="e73a7-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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


## <a name="cluster-management"></a><span data-ttu-id="e73a7-131">Управление кластерами</span><span class="sxs-lookup"><span data-stu-id="e73a7-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="e73a7-132">В этом разделе предполагается, что вы уже выполнили аутентификацию, создали экземпляр `HDInsightManagementClient` и сохранили его в переменной с именем `client`.</span><span class="sxs-lookup"><span data-stu-id="e73a7-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="e73a7-133">Инструкции по выполнению аутентификации и получению `HDInsightManagementClient` см. в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="e73a7-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="e73a7-134">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="e73a7-134">Create a Cluster</span></span>

<span data-ttu-id="e73a7-135">Кластер можно создать, вызвав `client.clusters.create()`.</span><span class="sxs-lookup"><span data-stu-id="e73a7-135">A new cluster can be created by calling `client.clusters.create()`.</span></span> 

#### <a name="example"></a><span data-ttu-id="e73a7-136">Пример</span><span class="sxs-lookup"><span data-stu-id="e73a7-136">Example</span></span>

<span data-ttu-id="e73a7-137">В этом примере показано, как создать кластер Spark с двумя головными узлами и одним рабочим.</span><span class="sxs-lookup"><span data-stu-id="e73a7-137">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="e73a7-138">Сначала необходимо создать группу ресурсов и учетную запись хранения, как описано далее.</span><span class="sxs-lookup"><span data-stu-id="e73a7-138">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="e73a7-139">Если они уже созданы, следующие шаги можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="e73a7-139">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="e73a7-140">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e73a7-140">Creating a Resource Group</span></span>

<span data-ttu-id="e73a7-141">Группу ресурсов можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-141">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="e73a7-142">Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="e73a7-142">Creating a Storage Account</span></span>

<span data-ttu-id="e73a7-143">Учетную запись хранения можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-143">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="e73a7-144">Теперь выполните такую команду, чтобы получить ключ для учетной записи хранения (он потребуется для создания кластера):</span><span class="sxs-lookup"><span data-stu-id="e73a7-144">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="e73a7-145">Показанный ниже фрагмент кода Python создает кластер Spark с двумя головными узлами и одним рабочим.</span><span class="sxs-lookup"><span data-stu-id="e73a7-145">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="e73a7-146">Задайте переменные, как описано в комментариях, и при необходимости измените другие параметры.</span><span class="sxs-lookup"><span data-stu-id="e73a7-146">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="e73a7-147">Получение сведений о кластере</span><span class="sxs-lookup"><span data-stu-id="e73a7-147">Get Cluster Details</span></span>

<span data-ttu-id="e73a7-148">Чтобы получить сведения о свойствах кластера, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-148">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e73a7-149">Пример</span><span class="sxs-lookup"><span data-stu-id="e73a7-149">Example</span></span>

<span data-ttu-id="e73a7-150">Чтобы убедиться в том, что вы создали кластер, можно использовать `get`.</span><span class="sxs-lookup"><span data-stu-id="e73a7-150">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="e73a7-151">Выходные данные должны выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="e73a7-151">The output should look like:</span></span>

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="e73a7-152">Получение списка кластеров</span><span class="sxs-lookup"><span data-stu-id="e73a7-152">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="e73a7-153">Получение списка кластеров в пределах подписки</span><span class="sxs-lookup"><span data-stu-id="e73a7-153">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="e73a7-154">Получение списка кластеров в пределах в группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e73a7-154">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="e73a7-155">`list()` и `list_by_resource_group()` возвращают объект `ClusterPaged`.</span><span class="sxs-lookup"><span data-stu-id="e73a7-155">Both `list()` and `list_by_resource_group()` return an `ClusterPaged` object.</span></span> <span data-ttu-id="e73a7-156">Вызов `advance_page()` возвращает список кластеров на этой странице и перемещает объект `ClusterPaged` на следующую страницу.</span><span class="sxs-lookup"><span data-stu-id="e73a7-156">Calling `advance_page()` returns the a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="e73a7-157">Этот вызов можно повторять до тех пор, пока не будет получено исключение `StopIteration`, означающее отсутствие дальнейших страниц.</span><span class="sxs-lookup"><span data-stu-id="e73a7-157">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="e73a7-158">Пример</span><span class="sxs-lookup"><span data-stu-id="e73a7-158">Example</span></span>

<span data-ttu-id="e73a7-159">В следующем примере выводятся свойства всех кластеров в пределах текущей подписки:</span><span class="sxs-lookup"><span data-stu-id="e73a7-159">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="e73a7-160">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="e73a7-160">Delete a Cluster</span></span>

<span data-ttu-id="e73a7-161">Чтобы удалить кластер, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-161">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="e73a7-162">Обновление тегов кластера</span><span class="sxs-lookup"><span data-stu-id="e73a7-162">Update Cluster Tags</span></span>

<span data-ttu-id="e73a7-163">Вы можете обновить теги кластера так:</span><span class="sxs-lookup"><span data-stu-id="e73a7-163">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="e73a7-164">Пример</span><span class="sxs-lookup"><span data-stu-id="e73a7-164">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="scale-cluster"></a><span data-ttu-id="e73a7-165">Масштабирование кластера</span><span class="sxs-lookup"><span data-stu-id="e73a7-165">Scale Cluster</span></span>

<span data-ttu-id="e73a7-166">Вы можете масштабировать кластер, изменяя количество его рабочих узлов так:</span><span class="sxs-lookup"><span data-stu-id="e73a7-166">You can scale a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="e73a7-167">Мониторинг кластера</span><span class="sxs-lookup"><span data-stu-id="e73a7-167">Cluster Monitoring</span></span>

<span data-ttu-id="e73a7-168">Пакет Azure Management SDK для HDInsight также позволяет управлять мониторингом кластеров с помощью Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="e73a7-168">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="e73a7-169">Включение мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="e73a7-169">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="e73a7-170">Чтобы включить мониторинг OMS, требуется рабочая область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e73a7-170">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="e73a7-171">Если вы не создавали такую рабочую область, см. статью [Создание рабочей области Log Analytics на портале Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="e73a7-171">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="e73a7-172">Чтобы включить мониторинг OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-172">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="e73a7-173">Просмотр состояния мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="e73a7-173">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="e73a7-174">Чтобы узнать состояние мониторинга OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-174">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="e73a7-175">Отключение мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="e73a7-175">Disable OMS Monitoring</span></span>

<span data-ttu-id="e73a7-176">Чтобы отключить мониторинг OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-176">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="e73a7-177">Элемент "Действия скрипта"</span><span class="sxs-lookup"><span data-stu-id="e73a7-177">Script Actions</span></span>

<span data-ttu-id="e73a7-178">В кластерах HDInsight поддерживается метод конфигурации с использованием, действий скриптов, который вызывает пользовательские скрипты для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="e73a7-178">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="e73a7-179">Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действий сценариев](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="e73a7-179">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="e73a7-180">Выполнение действий скриптов</span><span class="sxs-lookup"><span data-stu-id="e73a7-180">Execute Script Actions</span></span>
<span data-ttu-id="e73a7-181">Для выполнения действий скриптов в указанном кластере:</span><span class="sxs-lookup"><span data-stu-id="e73a7-181">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="e73a7-182">Удаление действий скриптов</span><span class="sxs-lookup"><span data-stu-id="e73a7-182">Delete Script Action</span></span>

<span data-ttu-id="e73a7-183">Чтобы удалить сохраненные действия скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-183">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="e73a7-184">Получение списка сохраненных действий скриптов</span><span class="sxs-lookup"><span data-stu-id="e73a7-184">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="e73a7-185">Методы `list()` и `list_persisted_scripts()` возвращают объект `RuntimeScriptActionDetailPaged`.</span><span class="sxs-lookup"><span data-stu-id="e73a7-185">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="e73a7-186">Вызов `advance_page()` возвращает список объектов `RuntimeScriptActionDetail` на соответствующей странице и перемещает объект `RuntimeScriptActionDetailPaged` на следующую страницу.</span><span class="sxs-lookup"><span data-stu-id="e73a7-186">Calling `advance_page()` returns the a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="e73a7-187">Этот вызов можно повторять до тех пор, пока не будет получено исключение `StopIteration`, означающее отсутствие дальнейших страниц.</span><span class="sxs-lookup"><span data-stu-id="e73a7-187">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="e73a7-188">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="e73a7-188">See the example below.</span></span>

<span data-ttu-id="e73a7-189">Чтобы получить список всех сохраненных действий скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-189">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e73a7-190">Пример</span><span class="sxs-lookup"><span data-stu-id="e73a7-190">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="e73a7-191">Просмотр журнала выполнения всех скриптов</span><span class="sxs-lookup"><span data-stu-id="e73a7-191">List All Scripts' Execution History</span></span>

<span data-ttu-id="e73a7-192">Чтобы получить журнал выполнения всех скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="e73a7-192">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e73a7-193">Пример</span><span class="sxs-lookup"><span data-stu-id="e73a7-193">Example</span></span>

<span data-ttu-id="e73a7-194">В этом примере выводятся сведения обо всех выполнявшихся скриптах.</span><span class="sxs-lookup"><span data-stu-id="e73a7-194">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```