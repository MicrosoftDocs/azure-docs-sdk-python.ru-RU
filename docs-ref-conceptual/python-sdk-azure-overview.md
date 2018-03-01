---
title: "Библиотеки Azure для Python"
description: "Обзор библиотек служб и библиотек управления Azure для Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 2b3e6d31edd7b946664853b3478e22205ab8c92e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/23/2018
---
# <a name="azure-libraries-for-python"></a>Библиотеки Azure для Python

Библиотеки Azure для Python позволяют использовать службы Azure и управлять ресурсами Azure в коде приложения. 

## <a name="manage-azure-resources"></a>Управление ресурсами Azure

Создавайте ресурсы Azure и управляйте ими из приложений Python, используя библиотеки Azure для Python.

Например, чтобы создать экземпляр SQL Server, можно использовать следующий код:

```python
sql_client = SqlManagementClient(
    credentials,
    subscription_id
)

server = sql_client.servers.create_or_update(
    'myresourcegroup',
    'myservername',
    {
        'location': 'eastus',
        'version': '12.0', # Required for create
        'administrator_login': 'mysecretname', # Required for create
        'administrator_login_password': 'HusH_Sec4et' # Required for create
    }
)
```

Полный список библиотек и рекомендации по их импорту в проекты см. в [инструкциях по установке](python-sdk-azure-install.md). А сведения по настройке проверки подлинности и выполнению примера кода в подписке Azure см. в [статье по началу работы](python-sdk-azure-get-started.yml).

## <a name="connect-to-azure-services"></a>Подключение к службам Azure

Библиотеки Python можно использовать не только для создания ресурсов и управления ими в Azure, но и для подключения и использования этих ресурсов в приложениях. Например, для обновления табличной базы данных SQL или хранения файлов в службе хранилища Azure. Выберите библиотеку, необходимую для конкретной службы, в полном списке библиотек и ознакомьтесь с руководствами и примерами кода, которые помогут вам использовать библиотеки в приложениях, в центре разработчиков Python.

Например, чтобы отправить простую HTML-страницу в большой двоичный объект и получить URL-адрес, используйте следующий код:

```python
storage_client = CloudStorageAccount(storage_account_name, storage_key)
blob_service = storage_client.create_block_blob_service()

blob_service.create_container(
    'mycontainername',
    public_access=PublicAccess.Blob
)

blob_service.create_blob_from_bytes(
    'mycontainername',
    'myblobname',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url('mycontainername', 'myblobname'))
```

## <a name="sample-code-and-reference"></a>Примеры кода и справочные материалы
В примерах кода ниже представлены общие задачи автоматизации, выполняемые с помощью библиотек управления Azure для Python. Это готовый код, который вы можете использовать в своих приложениях.
- [Виртуальные машины](python-sdk-azure-virtual-machine-samples.md)
- [Веб-приложения](python-sdk-azure-web-apps-samples.md)
- [База данных SQL](python-sdk-azure-sql-database-samples.md)

[Справочник](/python/api/overview/azure) доступен для всех пакетов в библиотеках служб и библиотеках управления. Сведения о новых функциях и критически важных изменениях, а также инструкции по переходу с предыдущих версий см. в [заметках о выпуске](python-sdk-azure-release-notes.md). 

## <a name="get-help-and-give-feedback"></a>Справка и отзывы

Задавайте вопросы сообществу на сайте [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) и описывайте проблемы с использованием пакета SDK на сайте [проекта GitHub](https://github.com/Azure/azure-sdk-for-python).
