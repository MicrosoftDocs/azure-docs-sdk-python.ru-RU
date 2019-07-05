---
title: Библиотеки ресурсов Azure для Python
description: ''
keywords: Azure, Python, SDK, API, Resources
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: d708a5e7296b166b6e55b9b7b0d995e72e264267
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534370"
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="9e236-103">Библиотеки ресурсов Azure для Python</span><span class="sxs-lookup"><span data-stu-id="9e236-103">Azure Resources libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="9e236-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9e236-104">Overview</span></span> 
<span data-ttu-id="9e236-105">Управление ресурсами Azure в группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9e236-105">Manage Azure resources in resource groups.</span></span>

| <span data-ttu-id="9e236-106">Package</span><span class="sxs-lookup"><span data-stu-id="9e236-106">Package</span></span>  |  <span data-ttu-id="9e236-107">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="9e236-107">Description</span></span> |
|---|---|
|<span data-ttu-id="9e236-108">[azure.mgmt.resource.features][1]</span><span class="sxs-lookup"><span data-stu-id="9e236-108">[azure.mgmt.resource.features][1]</span></span>|<span data-ttu-id="9e236-109">Azure Feature Exposure Control (AFEC) — это механизм для поставщиков ресурсов, который обеспечивает контроль над отображением функций пользователям.</span><span class="sxs-lookup"><span data-stu-id="9e236-109">Azure Feature Exposure Control (AFEC) provides a mechanism for the resource providers to control feature exposure to users.</span></span>|
|<span data-ttu-id="9e236-110">[azure.mgmt.resource.links][2]</span><span class="sxs-lookup"><span data-stu-id="9e236-110">[azure.mgmt.resource.links][2]</span></span>|<span data-ttu-id="9e236-111">Ресурсы Azure можно связывать друг с другом, формируя логические связи.</span><span class="sxs-lookup"><span data-stu-id="9e236-111">Azure resources can be linked together to form logical relationships.</span></span> <span data-ttu-id="9e236-112">Связи можно устанавливать между ресурсами, принадлежащими к разным группам ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9e236-112">You can establish links between resources belonging to different resource groups.</span></span>|
|<span data-ttu-id="9e236-113">[azure.mgmt.resource.locks][3]</span><span class="sxs-lookup"><span data-stu-id="9e236-113">[azure.mgmt.resource.locks][3]</span></span>|<span data-ttu-id="9e236-114">Ресурсы Azure можно блокировать, чтобы другие пользователи из вашей организации не могли их удалить или изменить.</span><span class="sxs-lookup"><span data-stu-id="9e236-114">Azure resources can be locked to prevent other users in your organization from deleting or modifying resources.</span></span>|
|<span data-ttu-id="9e236-115">[azure.mgmt.resource.managedapplications][4]</span><span class="sxs-lookup"><span data-stu-id="9e236-115">[azure.mgmt.resource.managedapplications][4]</span></span>|<span data-ttu-id="9e236-116">Приложения (устройства), управляемые с помощью ARM.</span><span class="sxs-lookup"><span data-stu-id="9e236-116">ARM managed applications (appliances).</span></span>|
|<span data-ttu-id="9e236-117">[azure.mgmt.resource.policy][5]</span><span class="sxs-lookup"><span data-stu-id="9e236-117">[azure.mgmt.resource.policy][5]</span></span>|<span data-ttu-id="9e236-118">Для управления доступом к ресурсам и контроля над ним можно определить настраиваемые политики и назначить их в той или иной области.</span><span class="sxs-lookup"><span data-stu-id="9e236-118">To manage and control access to your resources, you can define customized policies and assign them at a scope.</span></span>|
|<span data-ttu-id="9e236-119">[azure.mgmt.resource.resources][6]</span><span class="sxs-lookup"><span data-stu-id="9e236-119">[azure.mgmt.resource.resources][6]</span></span>| <span data-ttu-id="9e236-120">Операции для работы с ресурсами и группами ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9e236-120">Provides operations for working with resources and resource groups.</span></span>|
|<span data-ttu-id="9e236-121">[azure.mgmt.resource.subscriptions][7]</span><span class="sxs-lookup"><span data-stu-id="9e236-121">[azure.mgmt.resource.subscriptions][7]</span></span>|<span data-ttu-id="9e236-122">Все ресурсы и группы ресурсов существуют в пределах подписок.</span><span class="sxs-lookup"><span data-stu-id="9e236-122">All resource groups and resources exist within subscriptions.</span></span> <span data-ttu-id="9e236-123">Эти операции позволяют получать сведения о подписках и клиентах.</span><span class="sxs-lookup"><span data-stu-id="9e236-123">These operation enable you get information about your subscriptions and tenants.</span></span>|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a><span data-ttu-id="9e236-124">Установка библиотек</span><span class="sxs-lookup"><span data-stu-id="9e236-124">Install the libraries</span></span> 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a><span data-ttu-id="9e236-125">Пример</span><span class="sxs-lookup"><span data-stu-id="9e236-125">Example</span></span>
<span data-ttu-id="9e236-126">Ниже приведен пример создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9e236-126">The following is an example of how to create a resource group.</span></span> 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

<span data-ttu-id="9e236-127">Ознакомьтесь с другими [примерами кода Python](https://azure.microsoft.com/resources/samples/?platform=python), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="9e236-127">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span> 