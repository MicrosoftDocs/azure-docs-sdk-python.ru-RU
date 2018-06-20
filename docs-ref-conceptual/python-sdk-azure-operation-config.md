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
# <a name="operation-config"></a>Конфигурация операций 

Методы, используемые с операциями, имеют дополнительные параметры, которые могут быть предоставлены в kwargs. Это называется operation_config.

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
