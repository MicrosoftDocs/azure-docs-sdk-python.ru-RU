---
title: "Установка"
description: "Установка пакета Azure SDK для Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 792feac12f8328e2467017530065350e347c59b7
ms.sourcegitcommit: 757bf84535fd9d8299c4b51ec92a5ab1926cb671
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/27/2018
---
# <a name="installation"></a><span data-ttu-id="1df20-104">Установка</span><span class="sxs-lookup"><span data-stu-id="1df20-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="1df20-105">Какой вариант и какую версию Python использовать</span><span class="sxs-lookup"><span data-stu-id="1df20-105">Which Python and which version to use</span></span>
<span data-ttu-id="1df20-106">Доступно несколько интерпретаторов Python, например:</span><span class="sxs-lookup"><span data-stu-id="1df20-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="1df20-107">CPython — стандартный и наиболее часто используемый интерпретатор Python;</span><span class="sxs-lookup"><span data-stu-id="1df20-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="1df20-108">PyPy — быстродействующий аналог интерпретатора CPython;</span><span class="sxs-lookup"><span data-stu-id="1df20-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="1df20-109">IronPython — интерпретатор Python, работающий на базе .net/CLR;</span><span class="sxs-lookup"><span data-stu-id="1df20-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="1df20-110">Jython — интерпретатор Python, работающий на базе виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="1df20-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="1df20-111">**CPython** (версия 2.7 или 3.4 и выше) и PyPy 5.4.0 протестированы и поддерживаются с пакетом SDK Azure для Python.</span><span class="sxs-lookup"><span data-stu-id="1df20-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="1df20-112">Где можно получить Python?</span><span class="sxs-lookup"><span data-stu-id="1df20-112">Where to get Python?</span></span>
<span data-ttu-id="1df20-113">Существует несколько способов получить CPython:</span><span class="sxs-lookup"><span data-stu-id="1df20-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="1df20-114">Непосредственно [отсюда](https://www.python.org/).</span><span class="sxs-lookup"><span data-stu-id="1df20-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="1df20-115">Из надежных дистрибутивов, таких как [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) или [ActiveState](https://www.activestate.com/).</span><span class="sxs-lookup"><span data-stu-id="1df20-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="1df20-116">Построение из исходного кода!</span><span class="sxs-lookup"><span data-stu-id="1df20-116">Build from source!</span></span>

<span data-ttu-id="1df20-117">При отсутствии особой необходимости мы рекомендуем использовать первые два варианта.</span><span class="sxs-lookup"><span data-stu-id="1df20-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="1df20-118">Установка с помощью pip</span><span class="sxs-lookup"><span data-stu-id="1df20-118">Installation with pip</span></span>

<span data-ttu-id="1df20-119">Вы можете установить библиотеку отдельно для каждой службы Azure:</span><span class="sxs-lookup"><span data-stu-id="1df20-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="1df20-120">Предварительные версии пакетов можно установить с помощью флага `--pre` :</span><span class="sxs-lookup"><span data-stu-id="1df20-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="1df20-121">Набор библиотек Azure также можно установить одной строкой с помощью пакета метаданных `azure` .</span><span class="sxs-lookup"><span data-stu-id="1df20-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="1df20-122">Мы опубликовали предварительную версию этого пакета, доступ к которому можно получить с помощью флага --pre:</span><span class="sxs-lookup"><span data-stu-id="1df20-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="1df20-123">Установка из GitHub</span><span class="sxs-lookup"><span data-stu-id="1df20-123">Install from GitHub</span></span>

<span data-ttu-id="1df20-124">Если вы хотите установить `azure` из исходного кода:</span><span class="sxs-lookup"><span data-stu-id="1df20-124">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install