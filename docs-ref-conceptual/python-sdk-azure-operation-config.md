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
ms.openlocfilehash: d7be7cd76d019c6741d93c04458376a9352e363b
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/28/2018
ms.locfileid: "30204263"
---
# <a name="operation-config"></a><span data-ttu-id="f045b-104">Конфигурация операций</span><span class="sxs-lookup"><span data-stu-id="f045b-104">Operation config</span></span> 

<span data-ttu-id="f045b-105">Методы, используемые с операциями, имеют дополнительные параметры, которые могут быть предоставлены в kwargs.</span><span class="sxs-lookup"><span data-stu-id="f045b-105">Methods on operations have extra parameters which can be provided in the kwargs.</span></span> <span data-ttu-id="f045b-106">Это называется operation_config.</span><span class="sxs-lookup"><span data-stu-id="f045b-106">This is called operation_config.</span></span>

<span data-ttu-id="f045b-107">Параметры конфигурации приложения:</span><span class="sxs-lookup"><span data-stu-id="f045b-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="f045b-108">Имя параметра</span><span class="sxs-lookup"><span data-stu-id="f045b-108">Parameter name</span></span>|<span data-ttu-id="f045b-109">type</span><span class="sxs-lookup"><span data-stu-id="f045b-109">Type</span></span>|<span data-ttu-id="f045b-110">Роль</span><span class="sxs-lookup"><span data-stu-id="f045b-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="f045b-111">проверка</span><span class="sxs-lookup"><span data-stu-id="f045b-111">verify</span></span> |`bool`|<span data-ttu-id="f045b-112">Проверка SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="f045b-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="f045b-113">Значение по умолчанию — True.</span><span class="sxs-lookup"><span data-stu-id="f045b-113">Default is True.</span></span>|
|  <span data-ttu-id="f045b-114">cert</span><span class="sxs-lookup"><span data-stu-id="f045b-114">cert</span></span> |`str`| <span data-ttu-id="f045b-115">Путь к локальному сертификату для проверки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="f045b-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="f045b-116">timeout</span><span class="sxs-lookup"><span data-stu-id="f045b-116">timeout</span></span> |`int`| <span data-ttu-id="f045b-117">Время ожидания для установки подключения к серверу в секундах.</span><span class="sxs-lookup"><span data-stu-id="f045b-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="f045b-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="f045b-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="f045b-119">Разрешение перенаправлений.</span><span class="sxs-lookup"><span data-stu-id="f045b-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="f045b-120">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="f045b-120">max_redirects</span></span>  |`int`| <span data-ttu-id="f045b-121">Максимальное допустимое число перенаправлений.</span><span class="sxs-lookup"><span data-stu-id="f045b-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="f045b-122">proxies</span><span class="sxs-lookup"><span data-stu-id="f045b-122">proxies</span></span>  |`dict` |<span data-ttu-id="f045b-123">Параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="f045b-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="f045b-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="f045b-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="f045b-125">Чтение параметров прокси-сервера из локальных переменных среды.</span><span class="sxs-lookup"><span data-stu-id="f045b-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="f045b-126">retries</span><span class="sxs-lookup"><span data-stu-id="f045b-126">retries</span></span>  |`int` | <span data-ttu-id="f045b-127">Общее число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="f045b-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="f045b-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="f045b-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="f045b-129">Включение журналов HTTP-протокола в режиме отладки (по умолчанию — False).</span><span class="sxs-lookup"><span data-stu-id="f045b-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
