---
title: Библиотеки службы хранилища Azure для Python
description: ''
keywords: Azure, Python, SDK, API, Storage
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: storage
ms.openlocfilehash: 1cafbe5558c49e238182b7efabeae6fcb96d43d8
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534198"
---
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="f1522-103">Библиотеки службы хранилища Azure для Python</span><span class="sxs-lookup"><span data-stu-id="f1522-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="f1522-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f1522-104">Overview</span></span>
- <span data-ttu-id="f1522-105">Чтение и запись объектов и файлов из [хранилища BLOB-объектов Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="f1522-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="f1522-106">Отправка и получение сообщений между подключенными к облаку приложениями с помощью [хранилища очередей Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage).</span><span class="sxs-lookup"><span data-stu-id="f1522-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="f1522-107">Чтение и запись больших объемов структурированных данных с помощью [хранилища таблиц Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage).</span><span class="sxs-lookup"><span data-stu-id="f1522-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="f1522-108">Общий доступ к хранилищу для приложений с помощью [хранилища файлов Azure](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage).</span><span class="sxs-lookup"><span data-stu-id="f1522-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="f1522-109">Библиотеки управления позволяют создавать, обновлять и администрировать учетные записи службы хранилища Azure, а также запрашивать и повторно создавать ключи доступа в коде Python.</span><span class="sxs-lookup"><span data-stu-id="f1522-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="f1522-110">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="f1522-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="f1522-111">Клиент</span><span class="sxs-lookup"><span data-stu-id="f1522-111">Client</span></span>

<span data-ttu-id="f1522-112">Клиентские библиотеки службы хранилища Azure содержат четыре пакета: для хранилищ BLOB-объектов, файлов, очередей и таблиц.</span><span class="sxs-lookup"><span data-stu-id="f1522-112">Azure Storage Client Libraries consist of 4 packages: Blob, File, Queue and Table.</span></span> <span data-ttu-id="f1522-113">Чтобы установить пакет больших двоичных объектов, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f1522-113">To install the blob package, run:</span></span>

```bash
pip install azure-storage-blob
```

### <a name="management"></a><span data-ttu-id="f1522-114">Управление</span><span class="sxs-lookup"><span data-stu-id="f1522-114">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="f1522-115">Пример</span><span class="sxs-lookup"><span data-stu-id="f1522-115">Example</span></span>
```python
from azure.storage.blob import BlockBlobService

blob_service = BlockBlobService(account_name, account_key)

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

## <a name="samples"></a><span data-ttu-id="f1522-116">Примеры</span><span class="sxs-lookup"><span data-stu-id="f1522-116">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="f1522-117">Начало работы с хранилищем BLOB-объектов Azure в Python</span><span class="sxs-lookup"><span data-stu-id="f1522-117">Get started with Azure Blob Storage in Python</span></span>](https://docs.microsoft.com/azure/storage/blobs/storage-python-how-to-use-blob-storage) | <span data-ttu-id="f1522-118">Создание, чтение, обновление и удаление файлов и объектов в хранилище Azure, а также ограничение доступа к ним.</span><span class="sxs-lookup"><span data-stu-id="f1522-118">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="f1522-119">Начало работы с хранилищем очередей Azure в Python</span><span class="sxs-lookup"><span data-stu-id="f1522-119">Get started with Azure Queue Storage in Python</span></span>](https://docs.microsoft.com/azure/storage/queues/storage-python-how-to-use-queue-storage) | <span data-ttu-id="f1522-120">Вставка, просмотр, получение и удаление сообщений в очередях хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f1522-120">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="f1522-121">Управление учетными записями хранения Azure</span><span class="sxs-lookup"><span data-stu-id="f1522-121">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="f1522-122">Создание, обновление и удаление учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="f1522-122">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="f1522-123">Извлечение и повторное создание ключей доступа к учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f1522-123">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="f1522-124">Ознакомьтесь с другими [примерами кода Python](https://azure.microsoft.com/resources/samples/?platform=python), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="f1522-124">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>
