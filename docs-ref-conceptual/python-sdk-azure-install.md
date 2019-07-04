---
title: Установка
description: Установка пакета Azure SDK для Python
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 478118642122d7c0c80b1ddf37b13f71d8ca3adc
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534459"
---
# <a name="installation"></a><span data-ttu-id="3165e-104">Установка</span><span class="sxs-lookup"><span data-stu-id="3165e-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="3165e-105">Какой вариант и какую версию Python использовать</span><span class="sxs-lookup"><span data-stu-id="3165e-105">Which Python and which version to use</span></span>

<span data-ttu-id="3165e-106">Доступно несколько интерпретаторов Python, например:</span><span class="sxs-lookup"><span data-stu-id="3165e-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="3165e-107">CPython — стандартный и наиболее часто используемый интерпретатор Python;</span><span class="sxs-lookup"><span data-stu-id="3165e-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="3165e-108">PyPy — быстродействующий аналог интерпретатора CPython;</span><span class="sxs-lookup"><span data-stu-id="3165e-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="3165e-109">IronPython — интерпретатор Python, работающий на базе .net/CLR;</span><span class="sxs-lookup"><span data-stu-id="3165e-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="3165e-110">Jython — интерпретатор Python, работающий на базе виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="3165e-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="3165e-111">**CPython** (версия 2.7 или 3.4 и выше) и PyPy 5.4.0 протестированы и поддерживаются с пакетом SDK Azure для Python.</span><span class="sxs-lookup"><span data-stu-id="3165e-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="3165e-112">Где можно получить Python?</span><span class="sxs-lookup"><span data-stu-id="3165e-112">Where to get Python?</span></span>

<span data-ttu-id="3165e-113">Существует несколько способов получить CPython:</span><span class="sxs-lookup"><span data-stu-id="3165e-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="3165e-114">Непосредственно [отсюда](https://www.python.org/).</span><span class="sxs-lookup"><span data-stu-id="3165e-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="3165e-115">Из надежных дистрибутивов, таких как [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) или [ActiveState](https://www.activestate.com/).</span><span class="sxs-lookup"><span data-stu-id="3165e-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="3165e-116">Построение из исходного кода!</span><span class="sxs-lookup"><span data-stu-id="3165e-116">Build from source!</span></span>

<span data-ttu-id="3165e-117">При отсутствии особой необходимости мы рекомендуем использовать первые два варианта.</span><span class="sxs-lookup"><span data-stu-id="3165e-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="3165e-118">Установка с помощью pip</span><span class="sxs-lookup"><span data-stu-id="3165e-118">Installation with pip</span></span>

<span data-ttu-id="3165e-119">Вы можете установить библиотеку отдельно для каждой службы Azure:</span><span class="sxs-lookup"><span data-stu-id="3165e-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="3165e-120">Предварительные версии пакетов можно установить с помощью флага `--pre` :</span><span class="sxs-lookup"><span data-stu-id="3165e-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="3165e-121">Набор библиотек Azure также можно установить одной строкой с помощью пакета метаданных `azure` .</span><span class="sxs-lookup"><span data-stu-id="3165e-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="3165e-122">Мы опубликовали предварительную версию этого пакета, доступ к которому можно получить с помощью флага --pre:</span><span class="sxs-lookup"><span data-stu-id="3165e-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="3165e-123">Установка из GitHub</span><span class="sxs-lookup"><span data-stu-id="3165e-123">Install from GitHub</span></span>

<span data-ttu-id="3165e-124">Если вы хотите установить `azure` из исходного кода:</span><span class="sxs-lookup"><span data-stu-id="3165e-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a><span data-ttu-id="3165e-125">Установка старой версии с помощью pip</span><span class="sxs-lookup"><span data-stu-id="3165e-125">Install an older version with pip</span></span>
<span data-ttu-id="3165e-126">Вы можете установить старую версию `azure`, указав для нее значение "azure==3.0.0".</span><span class="sxs-lookup"><span data-stu-id="3165e-126">You can install an older version of `azure` by specifying 'azure==3.0.0' version details.</span></span>
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a><span data-ttu-id="3165e-127">Проверка сведений установки пакета SDK с помощью pip</span><span class="sxs-lookup"><span data-stu-id="3165e-127">Check SDK installation details with pip</span></span>
<span data-ttu-id="3165e-128">Вы можете проверить расположение установки пакета SDK `azure`, сведения о версии и т. д.</span><span class="sxs-lookup"><span data-stu-id="3165e-128">You can check `azure` SDK installation location, version details etc.</span></span>
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a><span data-ttu-id="3165e-129">Удаление с помощью pip</span><span class="sxs-lookup"><span data-stu-id="3165e-129">To uninstall with pip</span></span>
<span data-ttu-id="3165e-130">Вы можете удалить все библиотеки Azure одной строкой с помощью пакета метаданных `azure`.</span><span class="sxs-lookup"><span data-stu-id="3165e-130">You can uninstall all Azure libraries in a single line using the `azure` meta-package.</span></span>
```bash
pip uninstall azure 
```
> [!NOTE]
> <span data-ttu-id="3165e-131">`pip uninstall azure`удаляет пакет метаданных `azure`, но сохраняет отдельные пакеты `azure-*` (и другие пакеты, например `adal` и `msrest`).</span><span class="sxs-lookup"><span data-stu-id="3165e-131">`pip uninstall azure`removes the `azure` meta-package but leaves the individual `azure-*` packages behind (and others, like `adal` and `msrest` ).</span></span> <span data-ttu-id="3165e-132">Особенность Python и pip заключается в том, что для всех пакетов, которые имеют зависимости, удаление исходного пакета не приведет к удалению зависимостей.</span><span class="sxs-lookup"><span data-stu-id="3165e-132">An aspect of Python and pip is that for all packages that have dependencies, uninstalling the initial package does not uninstall the dependencies.</span></span> <span data-ttu-id="3165e-133">Чтобы удалить пакет `azure-` и пакеты поддержки, выполните команду `pip freeze | grep 'azure-' | xargs pip uninstall -y` (а затем отдельно удалите adal, msrest и msrestazure).</span><span class="sxs-lookup"><span data-stu-id="3165e-133">To remove `azure-` and its supporting packages, run the command `pip freeze | grep 'azure-' | xargs pip uninstall -y` (and then perform individual uninstalls for adal, msrest, and msrestazure).</span></span>

