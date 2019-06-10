---
title: Пакет Azure SDK для конфигурации операций Python
description: C, вызываемый пакетом Azure SDK для Python
keywords: Azure, Python, SDK, API, exceptions
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 03/07/2018
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: adeb6aa8a2c363c3119e97503df9536fb0633b4c
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376865"
---
# <a name="operation-config"></a><span data-ttu-id="0de55-104">Конфигурация операций</span><span class="sxs-lookup"><span data-stu-id="0de55-104">Operation config</span></span> 

<span data-ttu-id="0de55-105">Методы, используемые с операциями, имеют дополнительные параметры, которые могут быть предоставлены в `kwargs`.</span><span class="sxs-lookup"><span data-stu-id="0de55-105">Methods on operations have extra parameters which can be provided in the `kwargs`.</span></span> <span data-ttu-id="0de55-106">Это называется operation_config.</span><span class="sxs-lookup"><span data-stu-id="0de55-106">This is called operation_config.</span></span>

<span data-ttu-id="0de55-107">Параметры конфигурации приложения:</span><span class="sxs-lookup"><span data-stu-id="0de55-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="0de55-108">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="0de55-108">Parameter name</span></span>|<span data-ttu-id="0de55-109">type</span><span class="sxs-lookup"><span data-stu-id="0de55-109">Type</span></span>|<span data-ttu-id="0de55-110">Роль</span><span class="sxs-lookup"><span data-stu-id="0de55-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="0de55-111">проверка</span><span class="sxs-lookup"><span data-stu-id="0de55-111">verify</span></span> |`bool`|<span data-ttu-id="0de55-112">Проверка SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="0de55-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="0de55-113">Значение по умолчанию — True.</span><span class="sxs-lookup"><span data-stu-id="0de55-113">Default is True.</span></span>|
|  <span data-ttu-id="0de55-114">cert</span><span class="sxs-lookup"><span data-stu-id="0de55-114">cert</span></span> |`str`| <span data-ttu-id="0de55-115">Путь к локальному сертификату для проверки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="0de55-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="0de55-116">timeout</span><span class="sxs-lookup"><span data-stu-id="0de55-116">timeout</span></span> |`int`| <span data-ttu-id="0de55-117">Время ожидания для установки подключения к серверу в секундах.</span><span class="sxs-lookup"><span data-stu-id="0de55-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="0de55-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="0de55-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="0de55-119">Разрешение перенаправлений.</span><span class="sxs-lookup"><span data-stu-id="0de55-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="0de55-120">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="0de55-120">max_redirects</span></span>  |`int`| <span data-ttu-id="0de55-121">Максимальное допустимое число перенаправлений.</span><span class="sxs-lookup"><span data-stu-id="0de55-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="0de55-122">proxies</span><span class="sxs-lookup"><span data-stu-id="0de55-122">proxies</span></span>  |`dict` |<span data-ttu-id="0de55-123">Параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="0de55-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="0de55-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="0de55-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="0de55-125">Чтение параметров прокси-сервера из локальных переменных среды.</span><span class="sxs-lookup"><span data-stu-id="0de55-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="0de55-126">retries</span><span class="sxs-lookup"><span data-stu-id="0de55-126">retries</span></span>  |`int` | <span data-ttu-id="0de55-127">Общее число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="0de55-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="0de55-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="0de55-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="0de55-129">Включение журналов HTTP-протокола в режиме отладки (по умолчанию — False).</span><span class="sxs-lookup"><span data-stu-id="0de55-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
