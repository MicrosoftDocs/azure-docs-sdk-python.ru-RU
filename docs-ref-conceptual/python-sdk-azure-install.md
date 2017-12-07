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
ms.openlocfilehash: 5ce4ef27667d45697200eef67be92c62812b3809
ms.sourcegitcommit: c57305dad01cad925faf50a64953c408429d4ca9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="installation"></a>Установка

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
