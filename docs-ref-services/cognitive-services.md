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
ms.openlocfilehash: 5890c2091f8456dd9b8bcb68f8a34eed3cae6e04
ms.sourcegitcommit: d7ad0e8b4ba4add5e6f63e6b9eac54ecccdc7090
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148174"
---
# <a name="azure-cognitive-services-modules-for-python"></a><span data-ttu-id="b9cf6-104">Модули Azure Cognitive Services для Python</span><span class="sxs-lookup"><span data-stu-id="b9cf6-104">Azure Cognitive Services modules for Python</span></span>

<span data-ttu-id="b9cf6-105">Добавьте функции распознавания изображений и лиц, анализа языка и поиска в приложения, веб-сайты и средства Python, используя модули Azure Cognitive Services для Python.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-105">Add image and face recognition, language analysis, and search to your Python apps, websites, and tools using the Azure Cognitive Services modules for Python.</span></span>

## <a name="vision-modules"></a><span data-ttu-id="b9cf6-106">Модули визуального распознавания</span><span class="sxs-lookup"><span data-stu-id="b9cf6-106">Vision modules</span></span>

### <a name="computer-vision"></a><span data-ttu-id="b9cf6-107">API Компьютерного зрения</span><span class="sxs-lookup"><span data-stu-id="b9cf6-107">Computer Vision</span></span> 

<span data-ttu-id="b9cf6-108">Предоставляет информацию о визуальном содержимом изображений:</span><span class="sxs-lookup"><span data-stu-id="b9cf6-108">Returns information about visual content found in an image:</span></span>

- <span data-ttu-id="b9cf6-109">Используйте добавление тегов, описания и модели, предназначенные для определенных сфер, для безошибочного определения и обозначения содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-109">Use tagging, descriptions, and domain-specific models to identify content and label it with confidence.</span></span>
- <span data-ttu-id="b9cf6-110">Используйте параметры для определения непристойных материалов и содержимого для взрослых, чтобы включить автоматическое ограничение такого содержимого.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-110">Apply adult/racy settings to enable automated restriction of adult content.</span></span>
- <span data-ttu-id="b9cf6-111">Определяйте типы изображений и цветовые схемы на фотографиях.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-111">Identify image types and color schemes in pictures.</span></span>

<span data-ttu-id="b9cf6-112">[Попробуйте средства компьютерного зрения](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) в браузере бесплатно.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-112">[Try Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) for free in your browser.</span></span>

<span data-ttu-id="b9cf6-113">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-113">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-computervision
```

<span data-ttu-id="b9cf6-114">См. дополнительные сведения об [API компьютерного зрения](/azure/cognitive-services/computer-vision/home) и начните работу с помощью [краткого руководства по API компьютерного зрения для Python](/azure/cognitive-services/computer-vision/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-114">[Learn more](/azure/cognitive-services/computer-vision/home) about the Computer Vision API and get started with the [Computer Vision API Python quickstart](/azure/cognitive-services/computer-vision/quickstarts/python).</span></span>

### <a name="content-moderator"></a><span data-ttu-id="b9cf6-115">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="b9cf6-115">Content Moderator</span></span>

<span data-ttu-id="b9cf6-116">Машинная модерация текста, видео и изображений, улучшенная с помощью средств пользовательской проверки.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-116">Machine-assisted moderation of text, video and images, augmented with human review tools.</span></span>

<span data-ttu-id="b9cf6-117">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-117">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-contentmoderator
```

<span data-ttu-id="b9cf6-118">См. дополнительные сведения о [Content Moderator](/azure/cognitive-services/content-moderator/overview).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-118">[Learn more](/azure/cognitive-services/content-moderator/overview) about the Content Moderator service.</span></span>

### <a name="custom-vision-service"></a><span data-ttu-id="b9cf6-119">Служба "Пользовательское визуальное распознавание"</span><span class="sxs-lookup"><span data-stu-id="b9cf6-119">Custom Vision Service</span></span>

<span data-ttu-id="b9cf6-120">Отправка изображений для обучения и настройка модели компьютерного зрения для определенного варианта использования.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-120">Upload images to train and customize a computer vision model for your specific use case.</span></span> <span data-ttu-id="b9cf6-121">После обучения модели можно использовать API для добавления тегов в изображения с помощью модели, а также оценивать результаты для оптимизации вашего классификатора.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-121">Once the model is trained, you can use the API to tag images using the model and evaluate the results to improve your classifier.</span></span>

<span data-ttu-id="b9cf6-122">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-122">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-vision-customvision
```

<span data-ttu-id="b9cf6-123">См. дополнительные сведения о [Пользовательской службе визуального распознавания](/azure/cognitive-services/Custom-Vision-Service/home) и начните работу с помощью [руководства по Пользовательской службе визуального распознавания для Python](/azure/cognitive-services/Custom-Vision-Service/python-tutorial).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-123">[Learn more](/azure/cognitive-services/Custom-Vision-Service/home) about the Custom Vision service and get started with the [Custom Vision Python tutorial](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span></span>

### <a name="face-api"></a><span data-ttu-id="b9cf6-124">API Распознавания лиц</span><span class="sxs-lookup"><span data-stu-id="b9cf6-124">Face API</span></span>

<span data-ttu-id="b9cf6-125">Распознавание, идентификация, анализ и группировка лиц, а также добавление к ним тегов на фотографиях.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-125">Detect, identify, analyze, organize, and tag faces in photos.</span></span> 

<span data-ttu-id="b9cf6-126">[Попробуйте API распознавания лиц](https://azure.microsoft.com/en-us/services/cognitive-services/face/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-126">[Try the Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in your browser.</span></span>

<span data-ttu-id="b9cf6-127">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-127">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install cognitive-face
```

<span data-ttu-id="b9cf6-128">См. дополнительные сведения об [API распознавания лиц](/azure/cognitive-services/face/overview) в [кратком руководстве по API распознавания лиц для Python](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-128">[Learn more](/azure/cognitive-services/face/overview) about the Face API and get started with the [Face API Python quickstart](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span></span>

## <a name="search-modules"></a><span data-ttu-id="b9cf6-129">Поиск модулей</span><span class="sxs-lookup"><span data-stu-id="b9cf6-129">Search modules</span></span>

### <a name="web-search"></a><span data-ttu-id="b9cf6-130">Поиск в Интернете</span><span class="sxs-lookup"><span data-stu-id="b9cf6-130">Web search</span></span>

<span data-ttu-id="b9cf6-131">Получайте веб-документы, индексированные с помощью API Bing для поиска в Интернете, и ограничивайте результаты по типу, дате создания и другим критериям.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-131">Retrieve web documents indexed by the Bing Web Search API and narrow down the results by result type, freshness and more.</span></span> 

<span data-ttu-id="b9cf6-132">[Попробуйте API Поиска в Интернете](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-132">[Try the Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in your browser.</span></span>

<span data-ttu-id="b9cf6-133">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-133">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-websearch
```

<span data-ttu-id="b9cf6-134">См. дополнительные сведения об [API Bing для поиска в Интернете](/azure/cognitive-services/bing-web-search/overview) и начните работу с помощью [краткого руководства по API Поиска в Интернете для Python](/azure/cognitive-services/bing-web-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-134">[Learn more](/azure/cognitive-services/bing-web-search/overview) about the Bing Web Search API and get started with the [Web Search API Python quickstart](/azure/cognitive-services/bing-web-search/quickstarts/python).</span></span>

### <a name="image-search"></a><span data-ttu-id="b9cf6-135">Поиск изображений</span><span class="sxs-lookup"><span data-stu-id="b9cf6-135">Image search</span></span>

<span data-ttu-id="b9cf6-136">Выполняйте поиск изображений и получайте эскизы, полные URL-адреса изображений, метаданные изображения и другие сведения в качестве результатов.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-136">Search for images and get thumbnails, full image URLs, image metadata and more in your results.</span></span>

<span data-ttu-id="b9cf6-137">[Попробуйте API Поиска изображений](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-137">[Try the Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in your browser.</span></span>

<span data-ttu-id="b9cf6-138">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-138">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-imagesearch
```

<span data-ttu-id="b9cf6-139">См. дополнительные сведения об [API Bing для поиска изображений](/azure/cognitive-services/bing-image-search/overview) и начните работу с помощью [краткого руководства по API Поиска изображений для Python](/azure/cognitive-services/bing-image-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-139">[Learn more](/azure/cognitive-services/bing-image-search/overview) about the Bing Image Search API and get started with the [Image Search API Python quickstart](/azure/cognitive-services/bing-image-search/quickstarts/python).</span></span>


### <a name="entity-search"></a><span data-ttu-id="b9cf6-140">Поиск сущностей</span><span class="sxs-lookup"><span data-stu-id="b9cf6-140">Entity search</span></span>

<span data-ttu-id="b9cf6-141">Выполняйте поиск наиболее важных сущностей (мест, лиц или вещей) по заданному условию поиска или расположению.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-141">Search for the most relevant entity (place, person, or thing) for a given search term or location.</span></span>

<span data-ttu-id="b9cf6-142">[Попробуйте API Поиска сущностей](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-142">[Try the Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in your browser.</span></span>

<span data-ttu-id="b9cf6-143">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-143">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-entitysearch
```

<span data-ttu-id="b9cf6-144">См. дополнительные сведения об [API Bing для поиска сущностей](/azure/cognitive-services/bing-entities-search/search-the-web) и начните работу с помощью [краткого руководства по API Поиска сущностей для Python](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-144">[Learn more](/azure/cognitive-services/bing-entities-search/search-the-web) about the Bing Entity Search API and get started with the [Entity Search API Python quickstart](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span></span>

### <a name="custom-search"></a><span data-ttu-id="b9cf6-145">Пользовательский поиск</span><span class="sxs-lookup"><span data-stu-id="b9cf6-145">Custom search</span></span>

<span data-ttu-id="b9cf6-146">Выполняйте пользовательский поиск в Интернете в соответствии с конкретным доменом поиска.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-146">Build and a custom web search that meets your specific search domain.</span></span>

<span data-ttu-id="b9cf6-147">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-147">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-customsearch
```

<span data-ttu-id="b9cf6-148">См. дополнительные сведения о [Пользовательском поиске Bing](/azure/cognitive-services/bing-custom-search/) и начните работу с помощью [краткого руководства по API пользовательского поиска Bing для Python](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-148">[Learn more](/azure/cognitive-services/bing-custom-search/) about the Bing Custom Search service and get started with querying your custom search from Python with the [Custom Search API Python quickstart](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span></span>

### <a name="video-search"></a><span data-ttu-id="b9cf6-149">Поиск видео</span><span class="sxs-lookup"><span data-stu-id="b9cf6-149">Video search</span></span>

<span data-ttu-id="b9cf6-150">Выполняйте поиск видео в Интернете и получайте в результатах метаданные со сведениями об авторе, кодировке, длительности и числу просмотров.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-150">Find videos across the web and get results with creator, encoding, length, and view count metadata.</span></span>

<span data-ttu-id="b9cf6-151">[Попробуйте API Bing для поиска видео](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-151">[Try the Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in your browser.</span></span>

<span data-ttu-id="b9cf6-152">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-152">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-videosearch
```

<span data-ttu-id="b9cf6-153">См. дополнительные сведения об [API Bing для поиска видео](/azure/cognitive-services/bing-video-search/search-the-web) и начните работу с помощью [краткого руководства по API Bing для поиска видео для Python](/azure/cognitive-services/bing-video-search/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-153">[Learn more](/azure/cognitive-services/bing-video-search/search-the-web) about the Bing Video Search service and get started with the [Video Search API Python quickstart](/azure/cognitive-services/bing-video-search/python).</span></span>


### <a name="news-search"></a><span data-ttu-id="b9cf6-154">Поиск новостей</span><span class="sxs-lookup"><span data-stu-id="b9cf6-154">News search</span></span>

<span data-ttu-id="b9cf6-155">Выполняйте поиск новостей в Интернете и работайте со статьями, связанными новостями, изображениями, а также метаданными, содержащими сведения о поставщике.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-155">Search the web for news articles and work with article, related news, images, and provider info metadata.</span></span>

<span data-ttu-id="b9cf6-156">[Попробуйте API Bing для поиска новостей](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-156">[Try the News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in your browser.</span></span>

<span data-ttu-id="b9cf6-157">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-157">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-search-newssearch
```

<span data-ttu-id="b9cf6-158">См. дополнительные сведения об [API Bing для поиска новостей](/azure/cognitive-services/bing-news-search/search-the-web) и начните работу с помощью [краткого руководства по API Bing для поиска новостей для Python](//azure/cognitive-services/bing-news-search/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-158">[Learn more](/azure/cognitive-services/bing-news-search/search-the-web) about the Bing News Search service and get started with the [News Search API Python quickstart](//azure/cognitive-services/bing-news-search/python).</span></span>


## <a name="language-modules"></a><span data-ttu-id="b9cf6-159">Модули языка</span><span class="sxs-lookup"><span data-stu-id="b9cf6-159">Language modules</span></span>

### <a name="text-analytics"></a><span data-ttu-id="b9cf6-160">Анализ текста</span><span class="sxs-lookup"><span data-stu-id="b9cf6-160">Text Analytics</span></span> 

<span data-ttu-id="b9cf6-161">API анализа текста — это облачная служба, которая предоставляет возможности обработки естественного языка в необработанном тексте.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-161">The Text Analytics API is a cloud-based service that provides  natural language processing over raw text.</span></span> <span data-ttu-id="b9cf6-162">API включает три основные функции:</span><span class="sxs-lookup"><span data-stu-id="b9cf6-162">The API includes three main functions:</span></span>

- <span data-ttu-id="b9cf6-163">Анализ мнений</span><span class="sxs-lookup"><span data-stu-id="b9cf6-163">Sentiment analysis</span></span>
- <span data-ttu-id="b9cf6-164">Извлечение ключевой фразы</span><span class="sxs-lookup"><span data-stu-id="b9cf6-164">Key phrase extraction</span></span>
- <span data-ttu-id="b9cf6-165">Определение языка</span><span class="sxs-lookup"><span data-stu-id="b9cf6-165">Language detection</span></span>

<span data-ttu-id="b9cf6-166">[Попробуйте API анализа текста](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-166">[Try the Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in your browser.</span></span>

<span data-ttu-id="b9cf6-167">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-167">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-language-textanalytics
```

<span data-ttu-id="b9cf6-168">См. дополнительные сведения об [API анализа текста](/azure/cognitive-services/text-analytics/overview) и начните работу с помощью [краткого руководства по API анализа текста для Python](/azure/cognitive-services/text-analytics/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-168">[Learn more](/azure/cognitive-services/text-analytics/overview) about the Text Analytics API and get started with the [Text Analytics API Python quickstart](/azure/cognitive-services/text-analytics/quickstarts/python).</span></span>


### <a name="spell-check"></a><span data-ttu-id="b9cf6-169">Проверка орфографии</span><span class="sxs-lookup"><span data-stu-id="b9cf6-169">Spell Check</span></span>

<span data-ttu-id="b9cf6-170">Выполняйте контекстные проверки грамматики и орфографии с помощью API проверки орфографии Bing.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-170">Perform contextual grammar and spell checking with the Bing Spell Check API.</span></span>

<span data-ttu-id="b9cf6-171">[Попробуйте API проверки орфографии](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="b9cf6-171">[Try the Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in your browser.</span></span>

<span data-ttu-id="b9cf6-172">Получите модуль Python с помощью [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="b9cf6-172">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```
pip install azure-cognitiveservices-language-spellcheck
```

<span data-ttu-id="b9cf6-173">См. дополнительные сведения об [API проверки орфографии](/azure/cognitive-services/bing-spell-check/proof-text) в [кратком руководстве по API проверки орфографии для Python](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="b9cf6-173">[Learn more](/azure/cognitive-services/bing-spell-check/proof-text) about the Spell Check API and get started with the [Spell Check API Python quickstart](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span></span>
