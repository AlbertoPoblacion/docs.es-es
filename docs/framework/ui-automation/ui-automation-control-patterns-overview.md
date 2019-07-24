---
title: Información general acerca de los patrones de control de UI Automation
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns
- UI Automation, control patterns
ms.assetid: cc229b33-234b-469b-ad60-f0254f32d45d
ms.openlocfilehash: 7587c8cd24197252506967208869bd454b4f27f2
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68400673"
---
# <a name="ui-automation-control-patterns-overview"></a>Información general acerca de los patrones de control de UI Automation
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener la información más [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]reciente acerca [de, consulte API de automatización de Windows: Automatización](https://go.microsoft.com/fwlink/?LinkID=156746)de la interfaz de usuario.  
  
 Esta introducción presenta los patrones de control de [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] . Los patrones de control proporcionan una manera de categorizar y exponer la funcionalidad de un control independientemente de su tipo o apariencia.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] utiliza patrones de control para representar comportamientos de control comunes. Por ejemplo, utilice el patrón de control Invoke para los controles que se puedan invocar (como los botones) y el patrón de control Scroll para los controles que tengan barras de desplazamiento (como los cuadros de lista, las vistas de lista o los cuadros combinados). Como cada patrón de control representa una funcionalidad independiente, se pueden combinar para describir el conjunto completo de funcionalidad que admite un control determinado.  
  
> [!NOTE]
>  Los controles agregados, creados con controles secundarios que proporcionan a [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] la funcionalidad que expone el objeto primario, deben implementar todos los patrones de control normalmente asociados con cada control secundario. En cambio, no es necesario que los controles secundarios implementen esos mismos patrones de control.  
  
<a name="uiautomation_control_pattern_includes"></a>   
## <a name="ui-automation-control-pattern-components"></a>Componentes de los patrones de control de Automatización de la interfaz de usuario  
 Los patrones de control admiten los métodos, propiedades, eventos y relaciones necesarios para definir una parte de funcionalidad discreta disponible en un control.  
  
- La relación entre un elemento de Automatización de la interfaz de usuario y su elemento primario, sus elementos secundarios y los del mismo nivel describe la estructura del elemento dentro del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] .  
  
- Los métodos permiten que los clientes de Automatización de la interfaz de usuario manipulen el control.  
  
- Las propiedades y los eventos ofrecen información sobre la funcionalidad del patrón de control, así como información sobre el estado del control.  
  
 Los patrones de control se relacionan con [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] de la misma forma en que las interfaces se relacionan con los objetos [!INCLUDE[TLA#tla_com](../../../includes/tlasharptla-com-md.md)] . En [!INCLUDE[TLA2#tla_com](../../../includes/tla2sharptla-com-md.md)], puede consultar un objeto para averiguar las interfaces que admite y luego usar esas interfaces para acceder a la funcionalidad. En [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], los clientes de Automatización de la interfaz de usuario pueden preguntar a un control qué patrones de control admite y, después, interactuar con el control mediante los métodos, propiedades, eventos y estructuras que exponen los patrones de control admitidos. Por ejemplo, para un cuadro de edición multilínea, los proveedores de Automatización de la interfaz de usuario implementan <xref:System.Windows.Automation.Provider.IScrollProvider>. Si un cliente sabe que un elemento <xref:System.Windows.Automation.AutomationElement> admite el patrón de control <xref:System.Windows.Automation.ScrollPattern> , puede utilizar las propiedades, los métodos y los eventos expuestos por este patrón de control para manipular el control o acceder a información sobre el control.  
  
<a name="uiautomation_control_pattern_client_provider"></a>   
## <a name="ui-automation-providers-and-clients"></a>Clientes y proveedores de Automatización de la interfaz de usuario  
 Los proveedores de Automatización de la interfaz de usuario implementan patrones de control para exponer el comportamiento adecuado de una parte concreta de la funcionalidad que admite el control.  
  
 Los clientes de Automatización de la interfaz de usuario acceden a métodos y propiedades de clases de patrones de control [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] y los usan para obtener información sobre [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]o para manipular [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Estas clases de patrones de control se encuentran en el espacio de nombres <xref:System.Windows.Automation> (por ejemplo, <xref:System.Windows.Automation.InvokePattern> y <xref:System.Windows.Automation.SelectionPattern>).  
  
 Los clientes <xref:System.Windows.Automation.AutomationElement> utilizan métodos ( <xref:System.Windows.Automation.AutomationElement.GetCurrentPropertyValue%2A?displayProperty=nameWithType> como o <xref:System.Windows.Automation.AutomationElement.GetCachedPropertyValue%2A?displayProperty=nameWithType>) o los descriptores de acceso Common Language Runtime (CLR) [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] para tener acceso a las propiedades de un patrón. Cada clase de patrón de control tiene un miembro de campo ( <xref:System.Windows.Automation.InvokePattern.Pattern?displayProperty=nameWithType> por <xref:System.Windows.Automation.SelectionPattern.Pattern?displayProperty=nameWithType>ejemplo, o) que identifica ese patrón de control y se puede pasar <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> como <xref:System.Windows.Automation.AutomationElement.GetCurrentPattern%2A> un parámetro a o para recuperar <xref:System.Windows.Automation.AutomationElement>ese patrón para un.  
  
<a name="uiautomation_control_patterns_dynamic"></a>   
## <a name="dynamic-control-patterns"></a>Patrones de control dinámicos  
 Algunos controles no siempre admiten el mismo conjunto de patrones de control. Se considera que los patrones de control se admiten cuando están disponibles para un cliente de Automatización de la interfaz de usuario. Por ejemplo, un cuadro de edición multilínea solo permite el desplazamiento vertical cuando contiene más líneas de texto de las se pueden mostrar en su área visible. El desplazamiento se deshabilita cuando se elimina el texto suficiente para que ya no sea necesario desplazarse. En este ejemplo, el patrón de control ScrollPattern se admite dinámicamente según el estado actual del control (la cantidad de texto que hay en el cuadro de edición).  
  
<a name="Control_Pattern_Classes_and_Interfaces"></a>   
## <a name="control-pattern-classes-and-interfaces"></a>Interfaces y clases de patrón de control  
 En la siguiente tabla se describen los patrones de control de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] . En la tabla también se enumeran las clases que usan los clientes de Automatización de la interfaz de usuario para acceder a los patrones de control, así como las interfaces que utilizan los proveedores de Automatización de la interfaz de usuario para implementarlos.  
  
|Clase de patrón de control|Interfaz del proveedor|DESCRIPCIÓN|  
|---------------------------|------------------------|-----------------|  
|<xref:System.Windows.Automation.DockPattern>|<xref:System.Windows.Automation.Provider.IDockProvider>|Se utiliza con los controles que se pueden acoplar en un contenedor de acoplamiento. Por ejemplo, las barras de herramientas o las paletas de herramientas.|  
|<xref:System.Windows.Automation.ExpandCollapsePattern>|<xref:System.Windows.Automation.Provider.IExpandCollapseProvider>|Se utiliza con los controles que pueden expandir o contraer. Por ejemplo, los elementos de menú de una aplicación como el menú **Archivo** .|  
|<xref:System.Windows.Automation.GridPattern>|<xref:System.Windows.Automation.Provider.IGridProvider>|Se utiliza con los controles que admiten la funcionalidad de cuadrícula, como el ajuste de tamaño y el movimiento a una celda concreta. Por ejemplo, la vista de iconos grandes del Explorador de Windows o las tablas simples sin encabezados de [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)].|  
|<xref:System.Windows.Automation.GridItemPattern>|<xref:System.Windows.Automation.Provider.IGridItemProvider>|Se utiliza con los controles que tienen celdas dentro de cuadrículas. Las celdas individuales deben admitir el patrón GridItem. Por ejemplo, cada celda de la vista de detalle de [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)] .|  
|<xref:System.Windows.Automation.InvokePattern>|<xref:System.Windows.Automation.Provider.IInvokeProvider>|Se utiliza con los controles que se pueden invocar, como un botón.|  
|<xref:System.Windows.Automation.MultipleViewPattern>|<xref:System.Windows.Automation.Provider.IMultipleViewProvider>|Se utiliza con los controles que pueden cambiar entre varias representaciones del mismo conjunto de información, datos o elementos secundarios. Por ejemplo, un control de vista de lista donde los datos están disponibles en vistas en miniaturas, mosaico, iconos, lista o de detalle.|  
|<xref:System.Windows.Automation.RangeValuePattern>|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|Se utiliza con los controles que tienen un intervalo de valores que se pueden aplicar al control. Por ejemplo, un control de número que contiene años podría tener un intervalo de 1900 a 2010, mientras que otro control de número que muestra meses tendría un intervalo de 1 a 12.|  
|<xref:System.Windows.Automation.ScrollPattern>|<xref:System.Windows.Automation.Provider.IScrollProvider>|Se utiliza con los controles que pueden realizar desplazamiento. Por ejemplo, un control que tiene barras de desplazamiento que están activas cuando hay más información que se puede mostrar en el área visible del control.|  
|<xref:System.Windows.Automation.ScrollItemPattern>|<xref:System.Windows.Automation.Provider.IScrollItemProvider>|Se utiliza con los controles que tienen elementos individuales en una lista que permite desplazamiento. Por ejemplo, un control de lista que tiene elementos individuales en la lista de desplazamiento, como un control de cuadro combinado.|  
|<xref:System.Windows.Automation.SelectionPattern>|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Se utiliza con los controles de contenedor de selección. Por ejemplo, los cuadros de lista y los cuadros combinados.|  
|<xref:System.Windows.Automation.SelectionItemPattern>|<xref:System.Windows.Automation.Provider.ISelectionItemProvider>|Se utiliza con los elementos individuales de controles de contenedor de selección, como cuadros de lista y cuadros combinados.|  
|<xref:System.Windows.Automation.TablePattern>|<xref:System.Windows.Automation.Provider.ITableProvider>|Se utiliza con los controles que tienen una cuadrícula e información de encabezado. Por ejemplo, hojas de cálculo de [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] .|  
|<xref:System.Windows.Automation.TableItemPattern>|<xref:System.Windows.Automation.Provider.ITableItemProvider>|Se utiliza con los elementos de una tabla.|  
|<xref:System.Windows.Automation.TextPattern>|<xref:System.Windows.Automation.Provider.ITextProvider>|Se utiliza con los controles de edición y documentos que exponen información textual.|  
|<xref:System.Windows.Automation.TogglePattern>|<xref:System.Windows.Automation.Provider.IToggleProvider>|Se utiliza con los controles donde se puede alternar el estado. Por ejemplo, casillas y elementos de menú que pueden activarse.|  
|<xref:System.Windows.Automation.TransformPattern>|<xref:System.Windows.Automation.Provider.ITransformProvider>|Se utiliza con los controles que se pueden cambiar de tamaño, mover y girar. Los usos típicos del patrón de control Transform se encuentran en diseñadores, formularios, editores gráficos y aplicaciones de dibujo.|  
|<xref:System.Windows.Automation.ValuePattern>|<xref:System.Windows.Automation.Provider.IValueProvider>|Permite que los clientes obtengan o establezcan un valor en los controles que no admiten un intervalo de valores. Por ejemplo, un selector de fecha y hora.|  
|<xref:System.Windows.Automation.WindowPattern>|<xref:System.Windows.Automation.Provider.IWindowProvider>|Expone información concreta de ventanas, un concepto fundamental para el sistema operativo [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] . Como ejemplos de controles que son ventanas se pueden mencionar las ventanas de aplicación de nivel superior ([!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)], [!INCLUDE[TLA#tla_winexpl](../../../includes/tlasharptla-winexpl-md.md)], etc.), las ventanas secundarias de [!INCLUDE[TLA#tla_mdi](../../../includes/tlasharptla-mdi-md.md)] y los cuadros de diálogo.|  
  
## <a name="see-also"></a>Vea también

- [Patrones de control de Automatización de la interfaz de usuario para clientes](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
- [Asignación de patrones de control para clientes de Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)
- [Información general sobre la Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/ui-automation-overview.md)
- [Propiedades de Automatización de la interfaz de usuario para clientes](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md)
- [Eventos de Automatización de la interfaz de usuario para clientes](../../../docs/framework/ui-automation/ui-automation-events-for-clients.md)
