---
title: Información general sobre tipos de control de UI Automation
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, control types
- control types, UI Automation
ms.assetid: 75159ef8-bd43-4d13-acb7-1f1fe9253160
ms.openlocfilehash: e9cbff2ec6496cabe827e075b737a8c6f16fee93
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59147724"
---
# <a name="ui-automation-control-types-overview"></a>Información general sobre tipos de control de UI Automation
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener información más reciente sobre [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: Automatización de interfaz de usuario](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] tipos de control son identificadores conocidos que pueden usarse para indicar qué tipo de control determinado representa un elemento, como un cuadro combinado o un botón.  
  
 El hecho de disponer de un identificador conocido ayuda a los dispositivos de tecnología de asistencia a determinar qué tipos de controles están disponibles en la [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] y cómo interactuar con los controles.  
  
<a name="UI_Automation_Control_Type_Requisites"></a>   
## <a name="ui-automation-control-type-requisites"></a>Requisitos de los tipos de control de la automatización de la interfaz de usuario  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] tipos de control proporcionan un conjunto de condiciones que deben cumplir los proveedores. Cuando se cumplen estas condiciones, el control puede usar el nombre de tipo de control específico. Cada tipo de control tiene condiciones para los siguientes elementos:  
  
-   [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] patrones de control: qué patrones de control deben ser compatibles, qué control patrones son opcionales, y qué patrones de control no deben ser compatibles con el control.  
  
-   [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] los valores de propiedad, se admiten los valores de propiedades.  
  
-   [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] estructura de árbol: necesario [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] estructura para el control de árbol.  
  
 Cuando un control cumple las condiciones de un tipo de control particular, el valor de la propiedad <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.ControlType%2A> indicará ese tipo de control.  
  
<a name="Current_UI_Automation_Control_Types"></a>   
## <a name="current-ui-automation-control-types"></a>Tipos actuales de control de automatización de la interfaz de usuario  
 La siguiente lista contiene el conjunto actual de tipos de control de [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] :  
  
-   [Compatibilidad de UI Automation para el tipo de control Button](../../../docs/framework/ui-automation/ui-automation-support-for-the-button-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Calendar](../../../docs/framework/ui-automation/ui-automation-support-for-the-calendar-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control CheckBox](../../../docs/framework/ui-automation/ui-automation-support-for-the-checkbox-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control ComboBox](../../../docs/framework/ui-automation/ui-automation-support-for-the-combobox-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control DataGrid](../../../docs/framework/ui-automation/ui-automation-support-for-the-datagrid-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control DataItem](../../../docs/framework/ui-automation/ui-automation-support-for-the-dataitem-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Document](../../../docs/framework/ui-automation/ui-automation-support-for-the-document-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Edit](../../../docs/framework/ui-automation/ui-automation-support-for-the-edit-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Group](../../../docs/framework/ui-automation/ui-automation-support-for-the-group-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Header](../../../docs/framework/ui-automation/ui-automation-support-for-the-header-control-type.md)  
  
-   [Compatibilidad de la UI Automation para el tipo de control HeaderItem](../../../docs/framework/ui-automation/ui-automation-support-for-the-headeritem-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Hyperlink](../../../docs/framework/ui-automation/ui-automation-support-for-the-hyperlink-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Image](../../../docs/framework/ui-automation/ui-automation-support-for-the-image-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control List](../../../docs/framework/ui-automation/ui-automation-support-for-the-list-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control ListItem](../../../docs/framework/ui-automation/ui-automation-support-for-the-listitem-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Menu](../../../docs/framework/ui-automation/ui-automation-support-for-the-menu-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control MenuBar](../../../docs/framework/ui-automation/ui-automation-support-for-the-menubar-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control MenuItem](../../../docs/framework/ui-automation/ui-automation-support-for-the-menuitem-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Pane](../../../docs/framework/ui-automation/ui-automation-support-for-the-pane-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control ProgressBar](../../../docs/framework/ui-automation/ui-automation-support-for-the-progressbar-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control RadioButton](../../../docs/framework/ui-automation/ui-automation-support-for-the-radiobutton-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control ScrollBar](../../../docs/framework/ui-automation/ui-automation-support-for-the-scrollbar-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Separator](../../../docs/framework/ui-automation/ui-automation-support-for-the-separator-control-type.md)  
  
-   [Compatibilidad de la UI Automation para el tipo de control Slider](../../../docs/framework/ui-automation/ui-automation-support-for-the-slider-control-type.md)  
  
-   [Compatibilidad de automatización de la IU para el tipo de control Spinner](../../../docs/framework/ui-automation/ui-automation-support-for-the-spinner-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control SplitButton](../../../docs/framework/ui-automation/ui-automation-support-for-the-splitbutton-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control StatusBar](../../../docs/framework/ui-automation/ui-automation-support-for-the-statusbar-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Tab](../../../docs/framework/ui-automation/ui-automation-support-for-the-tab-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control TabItem](../../../docs/framework/ui-automation/ui-automation-support-for-the-tabitem-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Table](../../../docs/framework/ui-automation/ui-automation-support-for-the-table-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Text](../../../docs/framework/ui-automation/ui-automation-support-for-the-text-control-type.md)  
  
-   [Compatibilidad de automatización de la interfaz de usuario para el tipo de control de posición](../../../docs/framework/ui-automation/ui-automation-support-for-the-thumb-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control TitleBar](../../../docs/framework/ui-automation/ui-automation-support-for-the-titlebar-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control ToolBar](../../../docs/framework/ui-automation/ui-automation-support-for-the-toolbar-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control ToolTip](../../../docs/framework/ui-automation/ui-automation-support-for-the-tooltip-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Tree](../../../docs/framework/ui-automation/ui-automation-support-for-the-tree-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control TreeItem](../../../docs/framework/ui-automation/ui-automation-support-for-the-treeitem-control-type.md)  
  
-   [Compatibilidad de UI Automation para el tipo de control Window](../../../docs/framework/ui-automation/ui-automation-support-for-the-window-control-type.md)  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Automation.ControlType>
