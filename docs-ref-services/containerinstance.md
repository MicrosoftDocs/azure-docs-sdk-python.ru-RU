---
title: Библиотеки службы "Экземпляры контейнеров Azure" для Python
description: Справочник по библиотекам службы "Экземпляры контейнеров Azure" для Python
keywords: Azure, python, SDK, API, ACI, container, instances
author: mmacy
manager: jeconnoc
ms.date: 06/04/2018
ms.author: marsma
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 09f39375e0e92b6d09a965c3972d772a1437d0d4
ms.sourcegitcommit: 8c70bfd95309c3a77a4c0f73373c1785d59cdd10
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/05/2018
ms.locfileid: "34761332"
---
# <a name="azure-container-instances-libraries-for-python"></a>Библиотеки службы "Экземпляры контейнеров Azure" для Python

Создавайте и администрируйте экземпляры контейнеров Azure с помощью библиотеки службы "Экземпляры контейнеров Azure" для Python. Дополнительные сведения см. в статье [Экземпляры контейнеров Azure](/azure/container-instances/container-instances-overview).

## <a name="management-apis"></a>API управления

Создавайте и администрируйте экземпляры контейнеров Azure с помощью библиотеки управления.

Установите пакет управления с помощью pip:

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a>Пример исходного кода

Чтобы просмотреть приведенные ниже примеры кода в контексте, перейдите к следующему репозиторию GitHub:

[Azure-Samples/aci-docs-sample-python](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a>Authentication

Одним из самых простых способов аутентификации клиентских пакетов SDK (например, клиентов Resource Manager и службы "Экземпляры контейнеров Azure") является [аутентификация на основе файла](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file). Для использования этого способа нужно задать переменную среды `AZURE_AUTH_LOCATION`, чтобы указать путь к файлу учетных данных. Использование аутентификации на основе файла

1. Создайте файл учетных данных с помощью [Azure CLI](/cli/azure) или [Cloud Shell](https://shell.azure.com/):

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Если вы создаете файл учетных данных с помощью [Cloud Shell](https://shell.azure.com/), скопируйте содержимое файла в локальный файл, доступный для вашего приложения Python.

2. Задайте для переменной среды `AZURE_AUTH_LOCATION` полный путь к созданному файлу учетных данных. Пример (Bash):

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Создав файл учетных данных и задав значение для переменной среды `AZURE_AUTH_LOCATION`, используйте метод `get_client_from_auth_file` модуля [client_factory][client_factory] для инициализации объектов [ResourceManagementClient][ResourceManagementClient] и [ContainerInstanceManagementClient][ContainerInstanceManagementClient].

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

Дополнительные сведения о доступных способах аутентификации в библиотеках управления Python для Azure см. в статье [Проверка подлинности с помощью библиотек управления Azure для Python](/python/azure/python-sdk-azure-authenticate).

## <a name="create-container-group---single-container"></a>Создание группы контейнеров с одним контейнером

В этом примере создается группа контейнеров с одним контейнером.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L140 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Создание группы контейнеров с несколькими контейнерами

В этом примере создается группа контейнеров с двумя контейнерами: контейнером приложения и контейнером расширения.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L143-L196 "Create multi-container group")]

## <a name="create-task-based-container-group"></a>Создание группы контейнеров на основе задач

В этом примере создается группа контейнеров с одним контейнером на основе задач. В этом примере показаны некоторые возможности:

* [Переопределение командной строки](/azure/container-instances/container-instances-restart-policy#command-line-override) — задается пользовательская командная строка, отличная от указанной в строке `CMD` в файле Docker контейнера. Так вы можете указать пользовательскую командную строку для выполнения при запуске контейнера, переопределив командную строку по умолчанию, встроенную в контейнер. Так как при запуске контейнера выполняется несколько команд, происходит следующее:

   Чтобы выполнить **одну команду** с несколькими аргументами командной строки, например `echo FOO BAR`, укажите их в качестве списка строк для свойства `command` [контейнера][Container]. Например: 

   `command = ['echo', 'FOO', 'BAR']`

   Если нужно использовать **несколько команд** (возможно) с несколькими аргументами, выполните сценарий оболочки и передайте связанные команды в виде аргумента. Например, в этом случае выполняются команды `echo` и `tail`:

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* [Переменные среды](/azure/container-instances/container-instances-environment-variables) — для контейнера в группе контейнеров указываются две переменные среды. Чтобы изменить поведение скрипта или приложения во время запуска, используйте переменные среды либо передайте динамические сведения приложению, выполняющемуся в контейнере.
* [Политика перезапуска](/azure/container-instances/container-instances-restart-policy) — в конфигурации контейнера для политики перезапуска задано значение "Never". Это полезно для контейнеров на основе задач, выполняемых в рамках пакетного задания.
* Опрос операции с использованием [AzureOperationPoller][AzureOperationPoller] — после вызова метода создания выполняется опрос операции, чтобы определить время ее завершения и получить журналы группы.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L199-L275 "Run a task-based container")]

## <a name="list-container-groups"></a>Получение списка групп контейнеров

В этом примере выводится список групп контейнеров в группе ресурсов и некоторые свойства группы контейнеров.

При отображении списка групп контейнеров для свойства [instance_view][instance_view] каждой возвращаемой группы задано значение `None`. Чтобы получить сведения о контейнерах в группе контейнеров, необходимо выполнить операцию [Get][containergroupoperations_get] для определенной группы контейнеров. Эта команда возвращает группу с заполненным свойством `instance_view`. Пример итерации контейнеров из группы контейнеров на основе свойства `instance_view` см. ниже в разделе [Получение сведений о существующей группе контейнеров](#get-an-existing-container-group).

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L278-L292 "List container groups")]

## <a name="get-an-existing-container-group"></a>Получение сведений о существующей группе контейнеров

В этом примере возвращаются данные определенной группы контейнеров из группы ресурсов и выводятся некоторые свойства (включая контейнеры) группы контейнеров, а также их значения.

[Операция Get][containergroupoperations_get] возвращает группу контейнеров с заполненным свойством [instance_view][instance_view], что позволяет выполнять итерацию по каждому контейнеру в группе. Свойство `instance_vew` группы контейнеров заполняет только операция `get`. При получении списка групп контейнеров в подписке или группе ресурсов это свойство не заполняется, так как операция может повлечь большие затраты, например, при получении списка сотен групп контейнеров, каждая из которых может содержать несколько контейнеров. Как упоминалось в разделе [Получение списка групп контейнеров](#list-container-groups), после операции `list` следует выполнить операцию `get` для конкретной группы контейнеров, чтобы получить сведения об ее экземпляре контейнера.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L295-L324 "Get container group")]

## <a name="delete-a-container-group"></a>Удаление группы контейнеров

В этом примере удаляется несколько групп контейнеров из группы ресурсов, а также сама группа ресурсов.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a>Дополнительная информация

* Исходный код для приведенных выше примеров можно найти на сайте GitHub:

  [Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]

* Дополнительные примеры кода для службы "Экземпляры контейнеров Azure":

  [Примеры кода Azure][samples-aci]

* Ознакомьтесь с другими [примерами кода Python][samples-python], которые можно использовать в приложениях.

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/python/api/overview/azure/containerinstance/management)

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