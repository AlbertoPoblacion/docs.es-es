---
title: Aspectos relacionados con subprocesos de la UI Automation
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, threading issues
- threading issues with UI Automation
ms.assetid: 0ab8d42c-5b8b-481b-b788-2caecc2f0191
ms.openlocfilehash: 83b8ec67cff7006e736e0f65a7339b340b20d458
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2019
ms.locfileid: "57678597"
---
# <a name="ui-automation-threading-issues"></a>Aspectos relacionados con subprocesos de la UI Automation
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener información más reciente sobre [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: Automatización de interfaz de usuario](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Debido a la forma en que [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] utiliza los mensajes de Windows, pueden producirse conflictos cuando una aplicación cliente intenta interactuar con su propia [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] en el subproceso [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] . Estos conflictos pueden dar lugar a un rendimiento muy lento o incluso provocar que la aplicación deje de responder.  
  
 Si la aplicación cliente está diseñada para interactuar con todos los elementos del escritorio, incluida su propia [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)], debe realizar todas las llamadas a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] en un subproceso independiente. Esto incluye la ubicación de elementos (por ejemplo, mediante el método <xref:System.Windows.Automation.TreeWalker> o <xref:System.Windows.Automation.AutomationElement.FindAll%2A> ) y el uso de patrones de control.  
  
 Es seguro realizar llamadas a [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] dentro de un controlador de eventos de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , porque siempre se llama al controlador de eventos en un subproceso no de[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] . No obstante, al suscribirse a eventos que pueden provenir de la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]de la aplicación cliente, debe realizar la llamada a <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>, o a un método relacionado, en un subproceso no de[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] . Quite los controladores de eventos que estén en el mismo subproceso.
