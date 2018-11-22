---
title: Библиотеки мониторинга Azure для Python
description: Справочник по библиотекам мониторинга Azure для Python
keywords: Azure, python, SDK, API, Monitoring
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 2d4172fa206b89437cca88fb2c5d0a7965be4e9b
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277176"
---
# <a name="azure-monitoring-libraries-for-python"></a><span data-ttu-id="82672-104">Библиотеки мониторинга Azure для Python</span><span class="sxs-lookup"><span data-stu-id="82672-104">Azure Monitoring libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="82672-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="82672-105">Overview</span></span> 
<span data-ttu-id="82672-106">Мониторинг дает возможность отслеживать данные, чтобы обеспечить работоспособность приложения,</span><span class="sxs-lookup"><span data-stu-id="82672-106">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="82672-107">а также позволяет предотвратить потенциальные проблемы или устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="82672-107">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="82672-108">Кроме того, данные мониторинга можно использовать для получения подробных сведений о приложении.</span><span class="sxs-lookup"><span data-stu-id="82672-108">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="82672-109">Эти знания могут помочь повысить его производительность и улучшить возможности обслуживания, а также автоматизировать действия, которые в противном случае выполнялись бы вручную.</span><span class="sxs-lookup"><span data-stu-id="82672-109">That knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="82672-110">Дополнительные сведения о службе Azure Monitor см. [здесь](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="82672-110">Learn more about Azure Monitor [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span></span> 

## <a name="installation"></a><span data-ttu-id="82672-111">Установка</span><span class="sxs-lookup"><span data-stu-id="82672-111">Installation</span></span>
```bash
pip install azure-mgmt-monitor
```

## <a name="example---metrics"></a><span data-ttu-id="82672-112">Пример: метрики</span><span class="sxs-lookup"><span data-stu-id="82672-112">Example - Metrics</span></span>
<span data-ttu-id="82672-113">Этот пример кода получает метрики ресурсов Azure (виртуальных машин и т. д.).</span><span class="sxs-lookup"><span data-stu-id="82672-113">This sample obtains the metrics of a resource on Azure (VMs, etc.).</span></span> <span data-ttu-id="82672-114">В этом примере используется версия пакета Python не ниже 0.4.0.</span><span class="sxs-lookup"><span data-stu-id="82672-114">This sample requires version 0.4.0 of the Python package at least.</span></span>

<span data-ttu-id="82672-115">Полный список доступных ключевых слов для фильтров см. [здесь](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span><span class="sxs-lookup"><span data-stu-id="82672-115">A complete list of available keywords for filters is available [here](https://msdn.microsoft.com/library/azure/mt743622.aspx).</span></span>

<span data-ttu-id="82672-116">Поддерживаемые метрики для каждого типа ресурса см. [здесь](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span><span class="sxs-lookup"><span data-stu-id="82672-116">Supported metrics per resource type is available [here](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-supported-metrics).</span></span>

```python
import datetime
from azure.mgmt.monitor import MonitorManagementClient

# Get the ARM id of your resource. You might chose to do a "get"
# using the according management or to build the URL directly
# Example for a ARM VM
resource_id = (
    "subscriptions/{}/"
    "resourceGroups/{}/"
    "providers/Microsoft.Compute/virtualMachines/{}"
).format(subscription_id, resource_group_name, vm_name)

# create client
client = MonitorManagementClient(
    credentials,
    subscription_id
)

# You can get the available metrics of this specific resource
for metric in client.metric_definitions.list(resource_id):
    # azure.monitor.models.MetricDefinition
    print("{}: id={}, unit={}".format(
        metric.name.localized_value,
        metric.name.value,
        metric.unit
    ))

# Example of result for a VM:
# Percentage CPU: id=Percentage CPU, unit=Unit.percent
# Network In: id=Network In, unit=Unit.bytes
# Network Out: id=Network Out, unit=Unit.bytes
# Disk Read Bytes: id=Disk Read Bytes, unit=Unit.bytes
# Disk Write Bytes: id=Disk Write Bytes, unit=Unit.bytes
# Disk Read Operations/Sec: id=Disk Read Operations/Sec, unit=Unit.count_per_second
# Disk Write Operations/Sec: id=Disk Write Operations/Sec, unit=Unit.count_per_second

# Get CPU total of yesterday for this VM, by hour

today = datetime.datetime.now().date()
yesterday = today - datetime.timedelta(days=1)

metrics_data = client.metrics.list(
    resource_id,
    timespan="{}/{}".format(yesterday, today),
    interval='PT1H',
    metric='Percentage CPU',
    aggregation='Total'
)

for item in metrics_data.value:
    # azure.mgmt.monitor.models.Metric
    print("{} ({})".format(item.name.localized_value, item.unit.name))
    for timeserie in item.timeseries:
        for data in timeserie.data:
            # azure.mgmt.monitor.models.MetricData
            print("{}: {}".format(data.time_stamp, data.total))

# Example of result:
# Percentage CPU (percent)
# 2016-11-16 00:00:00+00:00: 72.0
# 2016-11-16 01:00:00+00:00: 90.59
# 2016-11-16 02:00:00+00:00: 60.58
# 2016-11-16 03:00:00+00:00: 65.78
# 2016-11-16 04:00:00+00:00: 43.96
# 2016-11-16 05:00:00+00:00: 43.96
# 2016-11-16 06:00:00+00:00: 114.9
# 2016-11-16 07:00:00+00:00: 45.4
```

## <a name="example---alerts"></a><span data-ttu-id="82672-117">Пример: оповещения</span><span class="sxs-lookup"><span data-stu-id="82672-117">Example - Alerts</span></span>
<span data-ttu-id="82672-118">В этом примере показано, как автоматически настраивать оповещения для ресурсов при их создании, чтобы обеспечить правильный мониторинг всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="82672-118">This example shows how to automatically set up alerts on your resources when they are created to ensure that all resources are monitored correctly.</span></span>

<span data-ttu-id="82672-119">Создайте на виртуальной машине источник данных для создания оповещений об использовании ЦП:</span><span class="sxs-lookup"><span data-stu-id="82672-119">Create a data source on a VM to alert on CPU usage:</span></span>
```python
from azure.mgmt.monitor import MonitorMgmtClient
from azure.mgmt.monitor.models import RuleMetricDataSource

resource_id = (
    "subscriptions/{}/"
    "resourceGroups/MonitorTestsDoNotDelete/"
    "providers/Microsoft.Compute/virtualMachines/MonitorTest"
).format(self.settings.SUBSCRIPTION_ID)

# create client
client = MonitorMgmtClient(
    credentials,
    subscription_id
)

# I need a subclass of "RuleDataSource"
data_source = RuleMetricDataSource(
    resource_uri = resource_id,
    metric_name = 'Percentage CPU'
)
```
<span data-ttu-id="82672-120">Создайте условие порогового значения, которое срабатывает, когда средняя загрузка ЦП виртуальной машины за последние 5 минут превышает 90 % (с использованием предыдущего источника данных):</span><span class="sxs-lookup"><span data-stu-id="82672-120">Create a threshold condition that triggers when the average CPU usage of a VM for the last 5 minutes is above 90% (using the preceding data source):</span></span>
```python
from azure.mgmt.monitor.models import ThresholdRuleCondition

# I need a subclasses of "RuleCondition"
rule_condition = ThresholdRuleCondition(
    data_source = data_source,
    operator = 'GreaterThanOrEqual',
    threshold = 90,
    window_size = 'PT5M',
    time_aggregation = 'Average'
)
```

<span data-ttu-id="82672-121">Создайте действие электронного сообщения:</span><span class="sxs-lookup"><span data-stu-id="82672-121">Create an email action:</span></span>
```python
from azure.mgmt.monitor.models import RuleEmailAction

# I need a subclass of "RuleAction"
rule_action = RuleEmailAction(
    send_to_service_owners = True,
    custom_emails = [
        'monitoringemail@microsoft.com'
    ]
)
```

<span data-ttu-id="82672-122">Создайте оповещение:</span><span class="sxs-lookup"><span data-stu-id="82672-122">Create the alert:</span></span>
```python
rule_name = 'MyPyTestAlertRule'
my_alert = client.alert_rules.create_or_update(
    group_name,
    rule_name,
    {
        'location': 'westus',
        'alert_rule_resource_name': rule_name,
        'description': 'Testing Alert rule creation',
        'is_enabled': True,
        'condition': rule_condition,
        'actions': [
            rule_action
        ]
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="82672-123">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="82672-123">Explore the Management APIs</span></span>](/python/api/overview/azure/monitoring/management)
