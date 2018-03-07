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
# <a name="installation"></a>Установка

## <a name="which-python-and-which-version-to-use"></a>Какой вариант и какую версию Python использовать
Доступно несколько интерпретаторов Python, например:

* CPython — стандартный и наиболее часто используемый интерпретатор Python;
* PyPy — быстродействующий аналог интерпретатора CPython;
* IronPython — интерпретатор Python, работающий на базе .net/CLR;
* Jython — интерпретатор Python, работающий на базе виртуальной машины Java.

**CPython** (версия 2.7 или 3.4 и выше) и PyPy 5.4.0 протестированы и поддерживаются с пакетом SDK Azure для Python.

## <a name="where-to-get-python"></a>Где можно получить Python?
Существует несколько способов получить CPython:

* Непосредственно [отсюда](https://www.python.org/).
* Из надежных дистрибутивов, таких как [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) или [ActiveState](https://www.activestate.com/).
* Построение из исходного кода!

При отсутствии особой необходимости мы рекомендуем использовать первые два варианта.

## <a name="installation-with-pip"></a>Установка с помощью pip

Вы можете установить библиотеку отдельно для каждой службы Azure:

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

Предварительные версии пакетов можно установить с помощью флага `--pre` :

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

Набор библиотек Azure также можно установить одной строкой с помощью пакета метаданных `azure` .

```bash
pip install azure
```

Мы опубликовали предварительную версию этого пакета, доступ к которому можно получить с помощью флага --pre:

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>Установка из GitHub

Если вы хотите установить `azure` из исходного кода:

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install