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
# <a name="hdinsight-sdk-for-python"></a><span data-ttu-id="36fbb-104">Пакет SDK HDInsight для Python</span><span class="sxs-lookup"><span data-stu-id="36fbb-104">HDInsight SDK for Python</span></span>

## <a name="overview"></a><span data-ttu-id="36fbb-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="36fbb-105">Overview</span></span>

<span data-ttu-id="36fbb-106">Пакет SDK HDInsight для Python предоставляет классы и методы для управления кластерами HDInsight.</span><span class="sxs-lookup"><span data-stu-id="36fbb-106">The HDInsight SDK for Python provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="36fbb-107">Пакет также поддерживает операции создания, удаления, обновления, получения списков, масштабирования, выполнения скриптов, мониторинга, получения свойства кластеров HDInsight и т. д.</span><span class="sxs-lookup"><span data-stu-id="36fbb-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36fbb-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="36fbb-108">Prerequisites</span></span>

* <span data-ttu-id="36fbb-109">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="36fbb-109">An Azure account.</span></span> <span data-ttu-id="36fbb-110">Если у вас ее нет, [получите бесплатную пробную версию](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="36fbb-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="36fbb-111">Python</span><span class="sxs-lookup"><span data-stu-id="36fbb-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="36fbb-112">pip</span><span class="sxs-lookup"><span data-stu-id="36fbb-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="36fbb-113">Установка пакета SDK</span><span class="sxs-lookup"><span data-stu-id="36fbb-113">SDK Installation</span></span>

<span data-ttu-id="36fbb-114">Пакет SDK HDInsight для Python можно найти на сайте [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) и установить с помощью команды:</span><span class="sxs-lookup"><span data-stu-id="36fbb-114">The HDInsight SDK for Python can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="36fbb-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="36fbb-115">Authentication</span></span>

<span data-ttu-id="36fbb-116">Для использования пакета SDK нужно выполнить аутентификацию с помощью подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="36fbb-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="36fbb-117">Ниже описано, как создать субъект-службу и использовать его для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="36fbb-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="36fbb-118">После этого вы получите экземпляр `HDInsightManagementClient`, в котором доступны различные методы (описанные далее) для операций управления.</span><span class="sxs-lookup"><span data-stu-id="36fbb-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="36fbb-119">Кроме описанного выше, есть и другие методы аутентификации, которые могут оказаться удобнее для вас.</span><span class="sxs-lookup"><span data-stu-id="36fbb-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="36fbb-120">Все способы описаны в статье [Проверка подлинности с помощью библиотек управления Azure для Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="36fbb-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="36fbb-121">Пример аутентификации с помощью субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="36fbb-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="36fbb-122">Сначала войдите в [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="36fbb-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="36fbb-123">Убедитесь, что вы используете подписку, в которой будет создан субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="36fbb-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="36fbb-124">Сведения о подписке отображаются в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="36fbb-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="36fbb-125">Если вы вошли не в ту подписку, выполните такую команду, чтобы выбрать правильную подписку:</span><span class="sxs-lookup"><span data-stu-id="36fbb-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="36fbb-126">Если вы еще не зарегистрировали поставщик ресурсов HDInsight с помощью другого метода (например, создав кластер HDInsight на портале Azure), вам необходимо это сделать, прежде чем выполнять аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="36fbb-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="36fbb-127">Это можно сделать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="36fbb-128">Создайте субъект-службу, выбрав имя и выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="36fbb-129">Сведения о субъекте-службе отображаются в виде JSON.</span><span class="sxs-lookup"><span data-stu-id="36fbb-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="36fbb-130">Скопируйте фрагмент кода Python ниже и задайте в качестве значений `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` и `SUBSCRIPTION_ID` строки из JSON-файла, возвращенного после выполнения команды для создания субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="36fbb-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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


## <a name="cluster-management"></a><span data-ttu-id="36fbb-131">Управление кластерами</span><span class="sxs-lookup"><span data-stu-id="36fbb-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="36fbb-132">В этом разделе предполагается, что вы уже выполнили аутентификацию, создали экземпляр `HDInsightManagementClient` и сохранили его в переменной с именем `client`.</span><span class="sxs-lookup"><span data-stu-id="36fbb-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="36fbb-133">Инструкции по выполнению аутентификации и получению `HDInsightManagementClient` см. в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="36fbb-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="36fbb-134">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="36fbb-134">Create a Cluster</span></span>

<span data-ttu-id="36fbb-135">Кластер можно создать, вызвав `client.clusters.create()`.</span><span class="sxs-lookup"><span data-stu-id="36fbb-135">A new cluster can be created by calling `client.clusters.create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="36fbb-136">Примеры</span><span class="sxs-lookup"><span data-stu-id="36fbb-136">Samples</span></span>

<span data-ttu-id="36fbb-137">Для создания нескольких распространенных типов кластеров HDInsight доступны примеры кода: [доступны примеры кода Python](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="36fbb-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight Python Samples](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="36fbb-138">Пример</span><span class="sxs-lookup"><span data-stu-id="36fbb-138">Example</span></span>

<span data-ttu-id="36fbb-139">В этом примере показано, как создать кластер Spark с двумя головными узлами и одним рабочим.</span><span class="sxs-lookup"><span data-stu-id="36fbb-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="36fbb-140">Сначала необходимо создать группу ресурсов и учетную запись хранения, как описано далее.</span><span class="sxs-lookup"><span data-stu-id="36fbb-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="36fbb-141">Если они уже созданы, следующие шаги можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="36fbb-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="36fbb-142">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="36fbb-142">Creating a Resource Group</span></span>

<span data-ttu-id="36fbb-143">Группу ресурсов можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="36fbb-144">Создание учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="36fbb-144">Creating a Storage Account</span></span>

<span data-ttu-id="36fbb-145">Учетную запись хранения можно создать с помощью [Azure Cloud Shell](https://shell.azure.com/bash), выполнив такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="36fbb-146">Теперь выполните такую команду, чтобы получить ключ для учетной записи хранения (он потребуется для создания кластера):</span><span class="sxs-lookup"><span data-stu-id="36fbb-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="36fbb-147">Показанный ниже фрагмент кода Python создает кластер Spark с двумя головными узлами и одним рабочим.</span><span class="sxs-lookup"><span data-stu-id="36fbb-147">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="36fbb-148">Задайте переменные, как описано в комментариях, и при необходимости измените другие параметры.</span><span class="sxs-lookup"><span data-stu-id="36fbb-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="36fbb-149">Получение сведений о кластере</span><span class="sxs-lookup"><span data-stu-id="36fbb-149">Get Cluster Details</span></span>

<span data-ttu-id="36fbb-150">Чтобы получить сведения о свойствах кластера, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-150">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="36fbb-151">Пример</span><span class="sxs-lookup"><span data-stu-id="36fbb-151">Example</span></span>

<span data-ttu-id="36fbb-152">Чтобы убедиться в том, что вы создали кластер, можно использовать `get`.</span><span class="sxs-lookup"><span data-stu-id="36fbb-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="36fbb-153">Выходные данные должны выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="36fbb-153">The output should look like:</span></span>

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="36fbb-154">Получение списка кластеров</span><span class="sxs-lookup"><span data-stu-id="36fbb-154">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="36fbb-155">Получение списка кластеров в пределах подписки</span><span class="sxs-lookup"><span data-stu-id="36fbb-155">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="36fbb-156">Получение списка кластеров в пределах в группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="36fbb-156">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="36fbb-157">Вызов `list()` и `list_by_resource_group()` возвращает объект `ClusterPaged`.</span><span class="sxs-lookup"><span data-stu-id="36fbb-157">Both `list()` and `list_by_resource_group()` return a `ClusterPaged` object.</span></span> <span data-ttu-id="36fbb-158">Вызов `advance_page()` возвращает список кластеров на этой странице и перемещает объект `ClusterPaged` на следующую страницу.</span><span class="sxs-lookup"><span data-stu-id="36fbb-158">Calling `advance_page()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="36fbb-159">Этот вызов можно повторять до тех пор, пока не будет получено исключение `StopIteration`, означающее отсутствие дальнейших страниц.</span><span class="sxs-lookup"><span data-stu-id="36fbb-159">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="36fbb-160">Пример</span><span class="sxs-lookup"><span data-stu-id="36fbb-160">Example</span></span>

<span data-ttu-id="36fbb-161">В следующем примере выводятся свойства всех кластеров в пределах текущей подписки:</span><span class="sxs-lookup"><span data-stu-id="36fbb-161">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="36fbb-162">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="36fbb-162">Delete a Cluster</span></span>

<span data-ttu-id="36fbb-163">Чтобы удалить кластер, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-163">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="36fbb-164">Обновление тегов кластера</span><span class="sxs-lookup"><span data-stu-id="36fbb-164">Update Cluster Tags</span></span>

<span data-ttu-id="36fbb-165">Вы можете обновить теги кластера так:</span><span class="sxs-lookup"><span data-stu-id="36fbb-165">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="36fbb-166">Пример</span><span class="sxs-lookup"><span data-stu-id="36fbb-166">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a><span data-ttu-id="36fbb-167">Изменение размера кластера</span><span class="sxs-lookup"><span data-stu-id="36fbb-167">Resize Cluster</span></span>

<span data-ttu-id="36fbb-168">Вы можете изменить размер кластера, изменяя количество его рабочих узлов. Укажите новый размер, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="36fbb-168">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="36fbb-169">Мониторинг кластера</span><span class="sxs-lookup"><span data-stu-id="36fbb-169">Cluster Monitoring</span></span>

<span data-ttu-id="36fbb-170">Пакет Azure Management SDK для HDInsight также позволяет управлять мониторингом кластеров с помощью Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="36fbb-170">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="36fbb-171">Включение мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="36fbb-171">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="36fbb-172">Чтобы включить мониторинг OMS, требуется рабочая область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="36fbb-172">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="36fbb-173">Если вы не создавали такую рабочую область, см. статью [Создание рабочей области Log Analytics на портале Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="36fbb-173">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="36fbb-174">Чтобы включить мониторинг OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-174">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="36fbb-175">Просмотр состояния мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="36fbb-175">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="36fbb-176">Чтобы узнать состояние мониторинга OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-176">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="36fbb-177">Отключение мониторинга OMS</span><span class="sxs-lookup"><span data-stu-id="36fbb-177">Disable OMS Monitoring</span></span>

<span data-ttu-id="36fbb-178">Чтобы отключить мониторинг OMS в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-178">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="36fbb-179">Элемент "Действия скрипта"</span><span class="sxs-lookup"><span data-stu-id="36fbb-179">Script Actions</span></span>

<span data-ttu-id="36fbb-180">В кластерах HDInsight поддерживается метод конфигурации с использованием, действий скриптов, который вызывает пользовательские скрипты для настройки кластера.</span><span class="sxs-lookup"><span data-stu-id="36fbb-180">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="36fbb-181">Дополнительные сведения о действиях скриптов см. в статье [Настройка кластеров HDInsight под управлением Linux с помощью действий сценариев](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="36fbb-181">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="36fbb-182">Выполнение действий скриптов</span><span class="sxs-lookup"><span data-stu-id="36fbb-182">Execute Script Actions</span></span>
<span data-ttu-id="36fbb-183">Для выполнения действий скриптов в указанном кластере:</span><span class="sxs-lookup"><span data-stu-id="36fbb-183">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="36fbb-184">Удаление действий скриптов</span><span class="sxs-lookup"><span data-stu-id="36fbb-184">Delete Script Action</span></span>

<span data-ttu-id="36fbb-185">Чтобы удалить сохраненные действия скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-185">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="36fbb-186">Получение списка сохраненных действий скриптов</span><span class="sxs-lookup"><span data-stu-id="36fbb-186">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="36fbb-187">Методы `list()` и `list_persisted_scripts()` возвращают объект `RuntimeScriptActionDetailPaged`.</span><span class="sxs-lookup"><span data-stu-id="36fbb-187">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="36fbb-188">Вызов `advance_page()` возвращает список объектов `RuntimeScriptActionDetail` на соответствующей странице и перемещает объект `RuntimeScriptActionDetailPaged` на следующую страницу.</span><span class="sxs-lookup"><span data-stu-id="36fbb-188">Calling `advance_page()` returns a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="36fbb-189">Этот вызов можно повторять до тех пор, пока не будет получено исключение `StopIteration`, означающее отсутствие дальнейших страниц.</span><span class="sxs-lookup"><span data-stu-id="36fbb-189">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="36fbb-190">См. пример ниже.</span><span class="sxs-lookup"><span data-stu-id="36fbb-190">See the example below.</span></span>

<span data-ttu-id="36fbb-191">Чтобы получить список всех сохраненных действий скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-191">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="36fbb-192">Пример</span><span class="sxs-lookup"><span data-stu-id="36fbb-192">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="36fbb-193">Просмотр журнала выполнения всех скриптов</span><span class="sxs-lookup"><span data-stu-id="36fbb-193">List All Scripts' Execution History</span></span>

<span data-ttu-id="36fbb-194">Чтобы получить журнал выполнения всех скриптов в кластере, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="36fbb-194">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="36fbb-195">Пример</span><span class="sxs-lookup"><span data-stu-id="36fbb-195">Example</span></span>

<span data-ttu-id="36fbb-196">В этом примере выводятся сведения обо всех выполнявшихся скриптах.</span><span class="sxs-lookup"><span data-stu-id="36fbb-196">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
