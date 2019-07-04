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

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a>Установка старой версии с помощью pip
Вы можете установить старую версию `azure`, указав для нее значение "azure==3.0.0".
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a>Проверка сведений установки пакета SDK с помощью pip
Вы можете проверить расположение установки пакета SDK `azure`, сведения о версии и т. д.
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a>Удаление с помощью pip
Вы можете удалить все библиотеки Azure одной строкой с помощью пакета метаданных `azure`.
```bash
pip uninstall azure 
```
> [!NOTE]
> `pip uninstall azure`удаляет пакет метаданных `azure`, но сохраняет отдельные пакеты `azure-*` (и другие пакеты, например `adal` и `msrest`). Особенность Python и pip заключается в том, что для всех пакетов, которые имеют зависимости, удаление исходного пакета не приведет к удалению зависимостей. Чтобы удалить пакет `azure-` и пакеты поддержки, выполните команду `pip freeze | grep 'azure-' | xargs pip uninstall -y` (а затем отдельно удалите adal, msrest и msrestazure).

