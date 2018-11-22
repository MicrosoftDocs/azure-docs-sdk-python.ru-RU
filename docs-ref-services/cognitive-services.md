---
title: Модули Azure Cognitive Services для Python
description: Справочник по модулям Azure Cognitive Services для Python
keywords: Azure, python, SDK, API, Cognitive Services
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/04/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 736b2dd747842caa50418afc8219dafae655db39
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277461"
---
# <a name="azure-cognitive-services-modules-for-python"></a>Модули Azure Cognitive Services для Python

Добавьте функции распознавания изображений и лиц, анализа языка и поиска в приложения, веб-сайты и средства Python, используя модули Azure Cognitive Services для Python.

## <a name="vision-modules"></a>Модули визуального распознавания

### <a name="computer-vision"></a>API компьютерного зрения 

Предоставляет информацию о визуальном содержимом изображений:

- Используйте добавление тегов, описания и модели, предназначенные для определенных сфер, для безошибочного определения и обозначения содержимого.
- Используйте параметры для определения непристойных материалов и содержимого для взрослых, чтобы включить автоматическое ограничение такого содержимого.
- Определяйте типы изображений и цветовые схемы на фотографиях.

[Попробуйте средства компьютерного зрения](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) в браузере бесплатно.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-computervision
```

См. дополнительные сведения об [API компьютерного зрения](/azure/cognitive-services/computer-vision/home) и начните работу с помощью [краткого руководства по API компьютерного зрения для Python](/azure/cognitive-services/computer-vision/quickstarts/python).

### <a name="content-moderator"></a>Content Moderator

Машинная модерация текста, видео и изображений, улучшенная с помощью средств пользовательской проверки.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-computervision
```

См. дополнительные сведения о [Content Moderator](/azure/cognitive-services/content-moderator/overview).

### <a name="custom-vision-service"></a>Пользовательская служба визуального распознавания

Отправка изображений для обучения и настройка модели компьютерного зрения для определенного варианта использования. После обучения модели можно использовать API для добавления тегов в изображения с помощью модели, а также оценивать результаты для оптимизации вашего классификатора.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-customvision
```

См. дополнительные сведения о [Пользовательской службе визуального распознавания](/azure/cognitive-services/Custom-Vision-Service/home) и начните работу с помощью [руководства по Пользовательской службе визуального распознавания для Python](/azure/cognitive-services/Custom-Vision-Service/python-tutorial).

### <a name="face-api"></a>API распознавания лиц

Распознавание, идентификация, анализ и группировка лиц, а также добавление к ним тегов на фотографиях. 

[Попробуйте API распознавания лиц](https://azure.microsoft.com/en-us/services/cognitive-services/face/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install cognitive-face
```

См. дополнительные сведения об [API распознавания лиц](/azure/cognitive-services/face/overview) в [кратком руководстве по API распознавания лиц для Python](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).

## <a name="search-modules"></a>Поиск модулей

### <a name="web-search"></a>Поиск в Интернете

Получайте веб-документы, индексированные с помощью API Bing для поиска в Интернете, и ограничивайте результаты по типу, дате создания и другим критериям. 

[Попробуйте API Поиска в Интернете](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-websearch
```

См. дополнительные сведения об [API Bing для поиска в Интернете](/azure/cognitive-services/bing-web-search/overview) и начните работу с помощью [краткого руководства по API Поиска в Интернете для Python](/azure/cognitive-services/bing-web-search/quickstarts/python).

### <a name="image-search"></a>Поиск изображений

Выполняйте поиск изображений и получайте эскизы, полные URL-адреса изображений, метаданные изображения и другие сведения в качестве результатов.

[Попробуйте API Поиска изображений](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-imagesearch
```

См. дополнительные сведения об [API Bing для поиска изображений](/azure/cognitive-services/bing-image-search/overview) и начните работу с помощью [краткого руководства по API Поиска изображений для Python](/azure/cognitive-services/bing-image-search/quickstarts/python).


### <a name="entity-search"></a>Поиск сущностей

Выполняйте поиск наиболее важных сущностей (мест, лиц или вещей) по заданному условию поиска или расположению.

[Попробуйте API Поиска сущностей](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-entitysearch
```

См. дополнительные сведения об [API Bing для поиска сущностей](/azure/cognitive-services/bing-entities-search/search-the-web) и начните работу с помощью [краткого руководства по API Поиска сущностей для Python](/azure/cognitive-services/bing-entities-search/quickstarts/python).

### <a name="custom-search"></a>Пользовательский поиск

Выполняйте пользовательский поиск в Интернете в соответствии с конкретным доменом поиска.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-customsearch
```

См. дополнительные сведения о [Пользовательском поиске Bing](/azure/cognitive-services/bing-custom-search/) и начните работу с помощью [краткого руководства по API пользовательского поиска Bing для Python](/azure/cognitive-services/bing-custom-search/call-endpoint-python).

### <a name="video-search"></a>Поиск видео

Выполняйте поиск видео в Интернете и получайте в результатах метаданные со сведениями об авторе, кодировке, длительности и числу просмотров.

[Попробуйте API Bing для поиска видео](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-videosearch
```

См. дополнительные сведения об [API Bing для поиска видео](/azure/cognitive-services/bing-video-search/search-the-web) и начните работу с помощью [краткого руководства по API Bing для поиска видео для Python](/azure/cognitive-services/bing-video-search/python).


### <a name="news-search"></a>Поиск новостей

Выполняйте поиск новостей в Интернете и работайте со статьями, связанными новостями, изображениями, а также метаданными, содержащими сведения о поставщике.

[Попробуйте API Bing для поиска новостей](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-newssearch
```

См. дополнительные сведения об [API Bing для поиска новостей](/azure/cognitive-services/bing-news-search/search-the-web) и начните работу с помощью [краткого руководства по API Bing для поиска новостей для Python](//azure/cognitive-services/bing-news-search/python).


## <a name="language-modules"></a>Модули языка

### <a name="text-analytics"></a>Текстовая аналитика 

API анализа текста — это облачная служба, которая предоставляет возможности обработки естественного языка в необработанном тексте. API включает три основные функции:

- Анализ мнений
- Извлечение ключевой фразы
- Определение языка

[Попробуйте API анализа текста](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-language-textanalytics
```

См. дополнительные сведения об [API анализа текста](/azure/cognitive-services/text-analytics/overview) и начните работу с помощью [краткого руководства по API анализа текста для Python](/azure/cognitive-services/text-analytics/quickstarts/python).


### <a name="spell-check"></a>Проверка орфографии

Выполняйте контекстные проверки грамматики и орфографии с помощью API проверки орфографии Bing.

[Попробуйте API проверки орфографии](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) в браузере.

Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-language-spellcheck
```

См. дополнительные сведения об [API проверки орфографии](/azure/cognitive-services/bing-spell-check/proof-text) в [кратком руководстве по API проверки орфографии для Python](/azure/cognitive-services/bing-spell-check/quickstarts/python).