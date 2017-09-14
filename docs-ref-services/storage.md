---
title: "Библиотеки службы хранилища Azure для Python"
description: 
keywords: Azure, Python, SDK, API, Storage
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: storage
ms.openlocfilehash: 64465964d32934a6a45dec44cb92a0a8a84b9c37
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-libraries-for-python"></a>Библиотеки службы хранилища Azure для Python

## <a name="overview"></a>Обзор
- Чтение и запись объектов и файлов из [хранилища BLOB-объектов Azure](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage).
- Отправка и получение сообщений между подключенными к облаку приложениями с помощью [хранилища очередей Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage).
- Чтение и запись больших объемов структурированных данных с помощью [хранилища таблиц Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage). 
- Общий доступ к хранилищу для приложений с помощью [хранилища файлов Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage).

Библиотеки управления позволяют создавать, обновлять и администрировать учетные записи службы хранилища Azure, а также запрашивать и повторно создавать ключи доступа в коде Python.

## <a name="install-the-libraries"></a>Установка библиотек

### <a name="client"></a>Клиент

```bash
pip install azure-storage
```

### <a name="management"></a>управления

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>Пример
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

## <a name="samples"></a>Примеры

| | |
|--|--|
| [Начало работы с хранилищем BLOB-объектов Azure в Python](https://azure.microsoft.com/resources/samples/storage-blob-python-getting-started/) | Создание, чтение, обновление и удаление файлов и объектов в хранилище Azure, а также ограничение доступа к ним. |
| [Начало работы с хранилищем очередей Azure в Python](https://azure.microsoft.com/resources/samples/storage-queue-python-getting-started/) | Вставка, просмотр, получение и удаление сообщений в очередях хранилища Azure. | 
| [Управление учетными записями хранения Azure](https://azure.microsoft.com/resources/samples/storage-python-manage) | Создание, обновление и удаление учетных записей хранения. Извлечение и повторное создание ключей доступа к учетной записи хранения.

Ознакомьтесь с другими [примерами кода Python](https://azure.microsoft.com/resources/samples/?platform=python), которые можно использовать в приложениях.