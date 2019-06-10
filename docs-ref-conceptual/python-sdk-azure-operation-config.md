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
# <a name="operation-config"></a>Конфигурация операций 

Методы, используемые с операциями, имеют дополнительные параметры, которые могут быть предоставлены в `kwargs`. Это называется operation_config.

Параметры конфигурации приложения:

|Имя параметра|type|Роль|
|----------------------|------|---------------|
| проверка |`bool`|Проверка SSL-сертификата. Значение по умолчанию — True.|
|  cert |`str`| Путь к локальному сертификату для проверки на стороне клиента.|
|  timeout |`int`| Время ожидания для установки подключения к серверу в секундах.|
|  allow_redirects |`bool` | Разрешение перенаправлений.|
|  allow_redirects  |`int`| Максимальное допустимое число перенаправлений.|
|  proxies  |`dict` |Параметры прокси-сервера.|
|  use_env_proxies |`bool` |Чтение параметров прокси-сервера из локальных переменных среды.|
|  retries  |`int` | Общее число повторных попыток.|
|  enable_http_logger | `bool`| Включение журналов HTTP-протокола в режиме отладки (по умолчанию — False).|
