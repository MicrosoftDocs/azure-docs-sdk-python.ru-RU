---
title: Библиотеки службы "Экземпляры контейнеров Azure" для Python
description: Справочник по библиотекам службы "Экземпляры контейнеров Azure" для Python
keywords: Azure, python, SDK, API, ACI, container, instances
author: dlepow
manager: jeconnoc
ms.date: 04/15/2019
ms.author: danlep
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 88df9443efb98bc5cec26c5eb4b01a4956141d40
ms.sourcegitcommit: 1b45953f168cbf36869c24c1741d70153b88b9fc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/17/2019
ms.locfileid: "59675939"
---
# <a name="azure-container-instances-libraries-for-python"></a><span data-ttu-id="7dd3e-104">Библиотеки службы "Экземпляры контейнеров Azure" для Python</span><span class="sxs-lookup"><span data-stu-id="7dd3e-104">Azure Container Instances libraries for Python</span></span>

<span data-ttu-id="7dd3e-105">Создавайте и администрируйте экземпляры контейнеров Azure с помощью библиотеки службы "Экземпляры контейнеров Azure" для Python.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-105">Use the Microsoft Azure Container Instances libraries for Python to create and manage Azure container instances.</span></span> <span data-ttu-id="7dd3e-106">Дополнительные сведения см. в статье [Экземпляры контейнеров Azure](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="7dd3e-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-apis"></a><span data-ttu-id="7dd3e-107">API управления</span><span class="sxs-lookup"><span data-stu-id="7dd3e-107">Management APIs</span></span>

<span data-ttu-id="7dd3e-108">Создавайте и администрируйте экземпляры контейнеров Azure с помощью библиотеки управления.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="7dd3e-109">Установите пакет управления с помощью pip:</span><span class="sxs-lookup"><span data-stu-id="7dd3e-109">Install the management package via pip:</span></span>

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a><span data-ttu-id="7dd3e-110">Пример исходного кода</span><span class="sxs-lookup"><span data-stu-id="7dd3e-110">Example source</span></span>

<span data-ttu-id="7dd3e-111">Чтобы просмотреть приведенные ниже примеры кода в контексте, перейдите к следующему репозиторию GitHub:</span><span class="sxs-lookup"><span data-stu-id="7dd3e-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="7dd3e-112">Azure-Samples/aci-docs-sample-python</span><span class="sxs-lookup"><span data-stu-id="7dd3e-112">Azure-Samples/aci-docs-sample-python</span></span>](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a><span data-ttu-id="7dd3e-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="7dd3e-113">Authentication</span></span>

<span data-ttu-id="7dd3e-114">Одним из самых простых способов аутентификации клиентских пакетов SDK (например, клиентов Resource Manager и службы "Экземпляры контейнеров Azure") является [аутентификация на основе файла](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span><span class="sxs-lookup"><span data-stu-id="7dd3e-114">One of the easiest ways to authenticate SDK clients (like the Azure Container Instances and Resource Manager clients in the following example) is with [file-based authentication](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span></span> <span data-ttu-id="7dd3e-115">Для использования этого способа нужно задать переменную среды `AZURE_AUTH_LOCATION`, чтобы указать путь к файлу учетных данных.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-115">File-based authentication queries the `AZURE_AUTH_LOCATION` environment variable for the path to a credentials file.</span></span> <span data-ttu-id="7dd3e-116">Использование аутентификации на основе файла</span><span class="sxs-lookup"><span data-stu-id="7dd3e-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="7dd3e-117">Создайте файл учетных данных с помощью [Azure CLI](/cli/azure) или [Cloud Shell](https://shell.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="7dd3e-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="7dd3e-118">Если вы создаете файл учетных данных с помощью [Cloud Shell](https://shell.azure.com/), скопируйте содержимое файла в локальный файл, доступный для вашего приложения Python.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your Python application can access.</span></span>

2. <span data-ttu-id="7dd3e-119">Задайте для переменной среды `AZURE_AUTH_LOCATION` полный путь к созданному файлу учетных данных.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="7dd3e-120">Пример (Bash):</span><span class="sxs-lookup"><span data-stu-id="7dd3e-120">For example (in Bash):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="7dd3e-121">Создав файл учетных данных и задав значение для переменной среды `AZURE_AUTH_LOCATION`, используйте метод `get_client_from_auth_file` модуля [client_factory][client_factory] для инициализации объектов [ResourceManagementClient][ResourceManagementClient] и [ContainerInstanceManagementClient][ContainerInstanceManagementClient].</span><span class="sxs-lookup"><span data-stu-id="7dd3e-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the `get_client_from_auth_file` method of the [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] and [ContainerInstanceManagementClient][ContainerInstanceManagementClient] objects.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

<span data-ttu-id="7dd3e-122">Дополнительные сведения о доступных способах аутентификации в библиотеках управления Python для Azure см. в статье [Проверка подлинности с помощью библиотек управления Azure для Python](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="7dd3e-122">For more details about the available authentication methods in the Python management libraries for Azure, see [Authenticate with the Azure Management Libraries for Python](/python/azure/python-sdk-azure-authenticate).</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="7dd3e-123">Создание группы контейнеров с одним контейнером</span><span class="sxs-lookup"><span data-stu-id="7dd3e-123">Create container group - single container</span></span>

<span data-ttu-id="7dd3e-124">В этом примере создается группа контейнеров с одним контейнером.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-124">This example creates a container group with a single container</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L141 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="7dd3e-125">Создание группы контейнеров с несколькими контейнерами</span><span class="sxs-lookup"><span data-stu-id="7dd3e-125">Create container group - multiple containers</span></span>

<span data-ttu-id="7dd3e-126">В этом примере создается группа контейнеров с двумя контейнерами: контейнером приложения и контейнером расширения.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-126">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L144-L197 "Create multi-container group")]

## <a name="create-task-based-container-group"></a><span data-ttu-id="7dd3e-127">Создание группы контейнеров на основе задач</span><span class="sxs-lookup"><span data-stu-id="7dd3e-127">Create task-based container group</span></span>

<span data-ttu-id="7dd3e-128">В этом примере создается группа контейнеров с одним контейнером на основе задач.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-128">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="7dd3e-129">В этом примере показаны некоторые возможности:</span><span class="sxs-lookup"><span data-stu-id="7dd3e-129">This example demonstrates several features:</span></span>

* <span data-ttu-id="7dd3e-130">[Переопределение командной строки](/azure/container-instances/container-instances-restart-policy#command-line-override) — задается пользовательская командная строка, отличная от указанной в строке `CMD` в файле Docker контейнера.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-130">[Command line override](/azure/container-instances/container-instances-restart-policy#command-line-override) - A custom command line, different from that which is specified in the container's Dockerfile `CMD` line, is specified.</span></span> <span data-ttu-id="7dd3e-131">Так вы можете указать пользовательскую командную строку для выполнения при запуске контейнера, переопределив командную строку по умолчанию, встроенную в контейнер.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-131">Command line override allows you to specify a custom command line to execute at container startup, overriding the default command line baked-in to the container.</span></span> <span data-ttu-id="7dd3e-132">Так как при запуске контейнера выполняется несколько команд, происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="7dd3e-132">Regarding executing multiple commands at container startup, the following applies:</span></span>

   <span data-ttu-id="7dd3e-133">Чтобы выполнить **одну команду** с несколькими аргументами командной строки, например `echo FOO BAR`, укажите их в качестве списка строк для свойства `command` [контейнера][Container].</span><span class="sxs-lookup"><span data-stu-id="7dd3e-133">If you want to run a **single command** with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string list to the `command` property of the [Container][Container].</span></span> <span data-ttu-id="7dd3e-134">Например: </span><span class="sxs-lookup"><span data-stu-id="7dd3e-134">For example:</span></span>

   `command = ['echo', 'FOO', 'BAR']`

   <span data-ttu-id="7dd3e-135">Если нужно использовать **несколько команд** (возможно) с несколькими аргументами, выполните сценарий оболочки и передайте связанные команды в виде аргумента.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-135">If, however, you want to run **multiple commands** with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="7dd3e-136">Например, в этом случае выполняются команды `echo` и `tail`:</span><span class="sxs-lookup"><span data-stu-id="7dd3e-136">For example, this executes both an `echo` and a `tail` command:</span></span>

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* <span data-ttu-id="7dd3e-137">[Переменные среды](/azure/container-instances/container-instances-environment-variables) — для контейнера в группе контейнеров указываются две переменные среды.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-137">[Environment variables](/azure/container-instances/container-instances-environment-variables) - Two environment variables are specified for the container in the container group.</span></span> <span data-ttu-id="7dd3e-138">Чтобы изменить поведение скрипта или приложения во время запуска, используйте переменные среды либо передайте динамические сведения приложению, выполняющемуся в контейнере.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-138">Use environment variables to modify script or application behavior at runtime, or otherwise pass dynamic information to an application running in the container.</span></span>
* <span data-ttu-id="7dd3e-139">[Политика перезапуска](/azure/container-instances/container-instances-restart-policy) — в конфигурации контейнера для политики перезапуска задано значение "Never". Это полезно для контейнеров на основе задач, выполняемых в рамках пакетного задания.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-139">[Restart policy](/azure/container-instances/container-instances-restart-policy) - The container is configured with a restart policy of "Never," useful for task-based containers that are executed as part of a batch job.</span></span>
* <span data-ttu-id="7dd3e-140">Опрос операции с использованием [AzureOperationPoller][AzureOperationPoller] — после вызова метода создания выполняется опрос операции, чтобы определить время ее завершения и получить журналы группы.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-140">Operation polling with [AzureOperationPoller][AzureOperationPoller] - After the create method is invoked, the operation is polled to determine when it has completed and the container group's logs can be obtained.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L200-L276 "Run a task-based container")]

## <a name="list-container-groups"></a><span data-ttu-id="7dd3e-141">Получение списка групп контейнеров</span><span class="sxs-lookup"><span data-stu-id="7dd3e-141">List container groups</span></span>

<span data-ttu-id="7dd3e-142">В этом примере выводится список групп контейнеров в группе ресурсов и некоторые свойства группы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-142">This example lists the container groups in a resource group and then prints a few of their properties.</span></span>

<span data-ttu-id="7dd3e-143">При отображении списка групп контейнеров для свойства [instance_view][instance_view] каждой возвращаемой группы задано значение `None`.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-143">When you list container groups,the [instance_view][instance_view] of each returned group is `None`.</span></span> <span data-ttu-id="7dd3e-144">Чтобы получить сведения о контейнерах в группе контейнеров, необходимо выполнить операцию [Get][containergroupoperations_get] для определенной группы контейнеров. Эта команда возвращает группу с заполненным свойством `instance_view`.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-144">To get the details of the containers within a container group, you must then [get][containergroupoperations_get] the container group, which returns the group with its `instance_view` property populated.</span></span> <span data-ttu-id="7dd3e-145">Пример итерации контейнеров из группы контейнеров на основе свойства `instance_view` см. ниже в разделе [Получение сведений о существующей группе контейнеров](#get-an-existing-container-group).</span><span class="sxs-lookup"><span data-stu-id="7dd3e-145">See the next section, [Get an existing container group](#get-an-existing-container-group), for an example of iterating over a container group's containers in its `instance_view`.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L279-L293 "List container groups")]

## <a name="get-an-existing-container-group"></a><span data-ttu-id="7dd3e-146">Получение сведений о существующей группе контейнеров</span><span class="sxs-lookup"><span data-stu-id="7dd3e-146">Get an existing container group</span></span>

<span data-ttu-id="7dd3e-147">В этом примере возвращаются данные определенной группы контейнеров из группы ресурсов и выводятся некоторые свойства (включая контейнеры) группы контейнеров, а также их значения.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-147">This example gets a specific container group from a resource group, and then prints a few of its properties (including its containers) and their values.</span></span>

<span data-ttu-id="7dd3e-148">[Операция Get][containergroupoperations_get] возвращает группу контейнеров с заполненным свойством [instance_view][instance_view], что позволяет выполнять итерацию по каждому контейнеру в группе.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-148">The [get operation][containergroupoperations_get] returns a container group with its [instance_view][instance_view] populated, which allows you to iterate over each container in the group.</span></span> <span data-ttu-id="7dd3e-149">Свойство `instance_vew` группы контейнеров заполняет только операция `get`. При получении списка групп контейнеров в подписке или группе ресурсов это свойство не заполняется, так как операция может повлечь большие затраты, например, при получении списка сотен групп контейнеров, каждая из которых может содержать несколько контейнеров.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-149">Only the `get` operation populates the `instance_vew` property of the container group--listing the container groups in a subscription or resource group doesn't populate the instance view due to the potentially expensive nature of the operation (for example, when listing hundreds of container groups, each potentially containing multiple containers).</span></span> <span data-ttu-id="7dd3e-150">Как упоминалось в разделе [Получение списка групп контейнеров](#list-container-groups), после операции `list` следует выполнить операцию `get` для конкретной группы контейнеров, чтобы получить сведения об ее экземпляре контейнера.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-150">As mentioned previously in the [List container groups](#list-container-groups) section, after a `list`, you must subsequently `get` a specific container group to obtain its container instance details.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L296-L325 "Get container group")]

## <a name="delete-a-container-group"></a><span data-ttu-id="7dd3e-151">Удаление группы контейнеров</span><span class="sxs-lookup"><span data-stu-id="7dd3e-151">Delete a container group</span></span>

<span data-ttu-id="7dd3e-152">В этом примере удаляется несколько групп контейнеров из группы ресурсов, а также сама группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-152">This example deletes several container groups from a resource group, as well as the resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a><span data-ttu-id="7dd3e-153">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="7dd3e-153">Next steps</span></span>

* <span data-ttu-id="7dd3e-154">Исходный код для приведенных выше примеров можно найти на сайте GitHub:</span><span class="sxs-lookup"><span data-stu-id="7dd3e-154">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="7dd3e-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span><span class="sxs-lookup"><span data-stu-id="7dd3e-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span></span>

* <span data-ttu-id="7dd3e-156">Дополнительные примеры кода для службы "Экземпляры контейнеров Azure":</span><span class="sxs-lookup"><span data-stu-id="7dd3e-156">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="7dd3e-157">[Примеры кода Azure][samples-aci]</span><span class="sxs-lookup"><span data-stu-id="7dd3e-157">[Azure Code Samples][samples-aci]</span></span>

* <span data-ttu-id="7dd3e-158">Ознакомьтесь с другими [примерами кода Python][samples-python], которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="7dd3e-158">Explore more [sample Python code][samples-python] you can use in your apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7dd3e-159">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="7dd3e-159">Explore the management APIs</span></span>](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient