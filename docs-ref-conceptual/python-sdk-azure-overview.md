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
# <a name="azure-libraries-for-python"></a><span data-ttu-id="de1ad-104">Библиотеки Azure для Python</span><span class="sxs-lookup"><span data-stu-id="de1ad-104">Azure libraries for Python</span></span>

<span data-ttu-id="de1ad-105">Библиотеки Azure для Python позволяют использовать службы Azure и управлять ресурсами Azure в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="de1ad-105">The Azure libraries for Python let you use Azure services and manage Azure resources from your application code.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="de1ad-106">Управление ресурсами Azure</span><span class="sxs-lookup"><span data-stu-id="de1ad-106">Manage Azure resources</span></span>

<span data-ttu-id="de1ad-107">Создавайте ресурсы Azure и управляйте ими из приложений Python, используя библиотеки Azure для Python.</span><span class="sxs-lookup"><span data-stu-id="de1ad-107">Create and manage Azure resources from Python applications using the Azure libraries for Python.</span></span>

<span data-ttu-id="de1ad-108">Например, чтобы создать экземпляр SQL Server, можно использовать следующий код:</span><span class="sxs-lookup"><span data-stu-id="de1ad-108">For example, to create a SQL Server instance, you can use the following code:</span></span>

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

<span data-ttu-id="de1ad-109">Полный список библиотек и рекомендации по их импорту в проекты см. в [инструкциях по установке](python-sdk-azure-install.md). А сведения по настройке проверки подлинности и выполнению примера кода в подписке Azure см. в [статье по началу работы](python-sdk-azure-get-started.yml).</span><span class="sxs-lookup"><span data-stu-id="de1ad-109">Review the [install instructions](python-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](python-sdk-azure-get-started.yml) to set up your authentication and run sample code against your own Azure subscription.</span></span>

## <a name="connect-to-azure-services"></a><span data-ttu-id="de1ad-110">Подключение к службам Azure</span><span class="sxs-lookup"><span data-stu-id="de1ad-110">Connect to Azure services</span></span>

<span data-ttu-id="de1ad-111">Библиотеки Python можно использовать не только для создания ресурсов и управления ими в Azure, но и для подключения и использования этих ресурсов в приложениях.</span><span class="sxs-lookup"><span data-stu-id="de1ad-111">In addition to using Python libraries to create and manage resources within Azure, you can also use Python libraries to connect and use those resources in your apps.</span></span> <span data-ttu-id="de1ad-112">Например, для обновления табличной базы данных SQL или хранения файлов в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="de1ad-112">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="de1ad-113">Выберите библиотеку, необходимую для конкретной службы, в полном списке библиотек и ознакомьтесь с руководствами и примерами кода, которые помогут вам использовать библиотеки в приложениях, в центре разработчиков Python.</span><span class="sxs-lookup"><span data-stu-id="de1ad-113">Select the library you need for a particular service from the complete list of libraries and visit the Python developer center for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="de1ad-114">Например, чтобы отправить простую HTML-страницу в большой двоичный объект и получить URL-адрес, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="de1ad-114">For example, to upload a simple HTML page on a blob and get the Url:</span></span>

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

## <a name="sample-code-and-reference"></a><span data-ttu-id="de1ad-115">Примеры кода и справочные материалы</span><span class="sxs-lookup"><span data-stu-id="de1ad-115">Sample code and reference</span></span>
<span data-ttu-id="de1ad-116">В примерах кода ниже представлены общие задачи автоматизации, выполняемые с помощью библиотек управления Azure для Python. Это готовый код, который вы можете использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="de1ad-116">The following samples cover common automation tasks with the Azure management libraries for Python and have code ready to use in your own apps:</span></span>
- [<span data-ttu-id="de1ad-117">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="de1ad-117">Virtual Machines</span></span>](python-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="de1ad-118">Веб-приложения</span><span class="sxs-lookup"><span data-stu-id="de1ad-118">Web apps</span></span>](python-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="de1ad-119">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="de1ad-119">SQL Database</span></span>](python-sdk-azure-sql-database-samples.md)

<span data-ttu-id="de1ad-120">[Справочник](/python/api/overview/azure) доступен для всех пакетов в библиотеках служб и библиотеках управления.</span><span class="sxs-lookup"><span data-stu-id="de1ad-120">A [reference](/python/api/overview/azure) is available for all packages in both the service an management libraries.</span></span> <span data-ttu-id="de1ad-121">Сведения о новых функциях и критически важных изменениях, а также инструкции по переходу с предыдущих версий см. в [заметках о выпуске](python-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="de1ad-121">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](python-sdk-azure-release-notes.md).</span></span> 

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="de1ad-122">Справка и отзывы</span><span class="sxs-lookup"><span data-stu-id="de1ad-122">Get help and give feedback</span></span>

<span data-ttu-id="de1ad-123">Задавайте вопросы сообществу на сайте [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) и описывайте проблемы с использованием пакета SDK на сайте [проекта GitHub](https://github.com/Azure/azure-sdk-for-python).</span><span class="sxs-lookup"><span data-stu-id="de1ad-123">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) and open issues against the SDK on the [project GitHub](https://github.com/Azure/azure-sdk-for-python).</span></span>
