---
title: Get started with auto scale by custom metric in Azure | Microsoft Docs
description: Learn how to scale your resource by custom metric in Azure.
author: rajram
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics

ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: rajram

---
# Get started with auto scale by custom metric in Azure
This article describes how to scale your resource by a custom metric in Azure portal.

Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments. 

# Lets get started
This article assumes that you have a web app with application insights configured. If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]

- Open [Azure portal][2]
- Click on Azure Monitor icon in the left navigation pane.
  ![Launch Azure Monitor][3]
- Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status
  ![Discover auto scale in Azure monitor][4]
- Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale
> Note: The steps below use an app service plan associated with a web app that has app insights configured.
- In the scale setting blade for the resource, notice that the current instance count is 1. Click on 'Enable autoscale'.
  ![Scale setting for new web app][5]
- Provide a name for the scale setting, and the click on "Add a rule". Notice the scale rule options that opens as a context pane in the right hand side. By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%. Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.
  ![Scale by custom metric][6]
- Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.
  ![Scale based on cpu][7]
- Set the you instance limits. For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'
> Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value. If the current capacity is already higher than default capacity, Autoscale will not scale in.
- Click on 'Save'

Congratulations. You now now succesfully created your scale setting to auto scale your web app based on a custom metric.

> Note: The same steps are applicable to get started with a VMSS or cloud service role.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
