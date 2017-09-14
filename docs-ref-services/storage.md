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
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="21ab8-103">Библиотеки службы хранилища Azure для Python</span><span class="sxs-lookup"><span data-stu-id="21ab8-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="21ab8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="21ab8-104">Overview</span></span>
- <span data-ttu-id="21ab8-105">Чтение и запись объектов и файлов из [хранилища BLOB-объектов Azure](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="21ab8-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="21ab8-106">Отправка и получение сообщений между подключенными к облаку приложениями с помощью [хранилища очередей Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage).</span><span class="sxs-lookup"><span data-stu-id="21ab8-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="21ab8-107">Чтение и запись больших объемов структурированных данных с помощью [хранилища таблиц Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage).</span><span class="sxs-lookup"><span data-stu-id="21ab8-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="21ab8-108">Общий доступ к хранилищу для приложений с помощью [хранилища файлов Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage).</span><span class="sxs-lookup"><span data-stu-id="21ab8-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="21ab8-109">Библиотеки управления позволяют создавать, обновлять и администрировать учетные записи службы хранилища Azure, а также запрашивать и повторно создавать ключи доступа в коде Python.</span><span class="sxs-lookup"><span data-stu-id="21ab8-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="21ab8-110">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="21ab8-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="21ab8-111">Клиент</span><span class="sxs-lookup"><span data-stu-id="21ab8-111">Client</span></span>

```bash
pip install azure-storage
```

### <a name="management"></a><span data-ttu-id="21ab8-112">управления</span><span class="sxs-lookup"><span data-stu-id="21ab8-112">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="21ab8-113">Пример</span><span class="sxs-lookup"><span data-stu-id="21ab8-113">Example</span></span>
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

## <a name="samples"></a><span data-ttu-id="21ab8-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="21ab8-114">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="21ab8-115">Начало работы с хранилищем BLOB-объектов Azure в Python</span><span class="sxs-lookup"><span data-stu-id="21ab8-115">Get started with Azure Blob Storage in Python</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-python-getting-started/) | <span data-ttu-id="21ab8-116">Создание, чтение, обновление и удаление файлов и объектов в хранилище Azure, а также ограничение доступа к ним.</span><span class="sxs-lookup"><span data-stu-id="21ab8-116">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="21ab8-117">Начало работы с хранилищем очередей Azure в Python</span><span class="sxs-lookup"><span data-stu-id="21ab8-117">Get started with Azure Queue Storage in Python</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-python-getting-started/) | <span data-ttu-id="21ab8-118">Вставка, просмотр, получение и удаление сообщений в очередях хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="21ab8-118">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="21ab8-119">Управление учетными записями хранения Azure</span><span class="sxs-lookup"><span data-stu-id="21ab8-119">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="21ab8-120">Создание, обновление и удаление учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="21ab8-120">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="21ab8-121">Извлечение и повторное создание ключей доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="21ab8-121">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="21ab8-122">Ознакомьтесь с другими [примерами кода Python](https://azure.microsoft.com/resources/samples/?platform=python), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="21ab8-122">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>