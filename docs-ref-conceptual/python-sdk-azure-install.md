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
# <a name="installation"></a><span data-ttu-id="4929a-104">Установка</span><span class="sxs-lookup"><span data-stu-id="4929a-104">Installation</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="4929a-105">Установка с помощью pip</span><span class="sxs-lookup"><span data-stu-id="4929a-105">Installation with pip</span></span>

<span data-ttu-id="4929a-106">Вы можете установить библиотеку отдельно для каждой службы Azure:</span><span class="sxs-lookup"><span data-stu-id="4929a-106">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="4929a-107">Предварительные версии пакетов можно установить с помощью флага `--pre` :</span><span class="sxs-lookup"><span data-stu-id="4929a-107">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="4929a-108">Набор библиотек Azure также можно установить одной строкой с помощью пакета метаданных `azure` .</span><span class="sxs-lookup"><span data-stu-id="4929a-108">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="4929a-109">Мы опубликовали предварительную версию этого пакета, доступ к которому можно получить с помощью флага --pre:</span><span class="sxs-lookup"><span data-stu-id="4929a-109">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="4929a-110">Установка из GitHub</span><span class="sxs-lookup"><span data-stu-id="4929a-110">Install from GitHub</span></span>

<span data-ttu-id="4929a-111">Если вы хотите установить `azure` из исходного кода:</span><span class="sxs-lookup"><span data-stu-id="4929a-111">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install
