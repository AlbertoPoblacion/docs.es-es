---
title: Compatibilidad de UI Automation para el tipo de control Menu
ms.date: 03/30/2017
helpviewer_keywords:
- control types, Menu
- UI Automation, Menu control type
- Menu control type
ms.assetid: 016323cb-f800-4938-b77b-2eb25d646090
ms.openlocfilehash: 9e8f0c07272fe3336c70d785b56f092b0e6cd068
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2019
ms.locfileid: "71041439"
---
# <a name="ui-automation-support-for-the-menu-control-type"></a>Compatibilidad de UI Automation para el tipo de control Menu
> [!NOTE]
> Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener la información más [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]reciente acerca [de, consulte API de automatización de Windows: Automatización](https://go.microsoft.com/fwlink/?LinkID=156746)de la interfaz de usuario.  
  
 En este tema se ofrece información sobre la compatibilidad de [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] con el tipo de control Menu. Describe la estructura de árbol de [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] de control y ofrece las propiedades y los patrones de control para escenarios de control concretos.  
  
 Un control de menú permite organizar jerárquicamente los elementos asociados a comandos y controladores de eventos. En una aplicación [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] típica, una barra de menús contiene varios botones de menú (como **Archivo**, **Editar**y **Ventana**) y cada botón de menú muestra un menú. Un menú contiene una colección de elementos de menú (como **Nuevo**, **Abrir**y **Cerrar**), que se puede expandir para mostrar elementos de menú adicionales o realizar una acción específica cuando se haga clic en ellos.  
  
 En las secciones siguientes se definen la estructura de árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] necesaria, las propiedades, los patrones de control y los eventos para el tipo de control Menu. Los requisitos [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] se aplican a todos los controles de lista, ya sean [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)]o [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## <a name="required-ui-automation-tree-structure"></a>Estructura de árbol de automatización de interfaz de usuario necesaria  
 En la tabla siguiente se describen la vista de control y la vista de contenido del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] que pertenece a los controles de menú y se describe lo que puede incluirse en cada vista. Para más información sobre el árbol [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , vea [UI Automation Tree Overview](ui-automation-tree-overview.md).  
  
|Vista de control|Vista de contenido|  
|------------------|------------------|  
|Menú<br /><br /> -MenuItem (1 o varios)|No aplicable (a menos que el control de menú sea un menú contextual que sea un elemento primario de un objeto que no sea un elemento de menú)<br /><br /> -MenuItem (1 o varios)|  
  
 Los controles de menú siempre aparecen en las vistas de control y contenido del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] . Los tipos de control de menú deben aparecer en el control al que hace referencia su información. Los clientes de Automatización de la interfaz de usuario deben estar a la escucha de `MenuOpenedEvent` para asegurarse de que obtienen de forma coherente la información que transmiten los controles de menú. Los controles de menú contextual son un caso especial. Aparecen como elementos secundarios del escritorio.  
  
<a name="Required_UI_Automation_Properties"></a>   
## <a name="required-ui-automation-properties"></a>Propiedades necesarias para la automatización de la interfaz de usuario  
 En la tabla siguiente se muestran las propiedades de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] que tienen un valor o una definición que es especialmente relevante para el tipo de control Menu. Para obtener más información [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] sobre las propiedades, vea [UI Automation Properties for clients](ui-automation-properties-for-clients.md).  
  
|Propiedad[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Valor|Notas|  
|------------------------------------------------------------------------------------|-----------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|No admitido|El control de menú no requiere que se establezca una propiedad Name.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|`Null`|No se espera ninguna etiqueta con un control de menú típico.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Menú|Este valor es el mismo para todos los marcos de trabajo de la interfaz de usuario.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|False|El control de menú no se incluye en la vista de contenido del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] .|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|El control de menú siempre se incluye en la vista de control del árbol de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] .|  
  
<a name="Required_UI_Automation_Control_Patterns"></a>   
## <a name="required-ui-automation-control-patterns"></a>Patrones de control necesarios para la automatización de la interfaz de usuario  
 No hay ningún patrón de control necesario para el tipo de control Menu.  
  
<a name="Required_UI_Automation_Events"></a>   
## <a name="required-ui-automation-events"></a>Eventos de automatización de la interfaz de usuario necesarios  
 Los controles de menú deben generar el evento `MenuOpenedEvent` cuando aparecen en la pantalla. El evento `MenuOpenedEvent` incluirá el texto del control. El evento `MenuClosedEvent` debe generarse cuando un menú desaparece de la pantalla.  
  
 En la siguiente tabla se muestran los eventos de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] que deben admitir todos los controles de menú. Para más información sobre eventos, vea [UI Automation Events Overview](ui-automation-events-overview.md).  
  
|o[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Soporte técnico/valor|Notas|  
|---------------------------------------------------------------------------------|--------------------|-----------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.MenuOpenedEvent>|Requerido|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.MenuClosedEvent>|Obligatorio|None|  
|Evento cambiado por propiedad<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty> .|Obligatorio|None|  
|Evento cambiado por propiedad<xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty> .|Obligatorio|None|  
|Evento cambiado por propiedad<xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty> .|Obligatorio|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Obligatorio|None|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Obligatorio|None|  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Automation.ControlType.Menu>
- [Información general sobre los patrones de control de la Automatización de la interfaz de usuario](ui-automation-control-patterns-overview.md)
- [Información general sobre tipos de control de Automatización de la interfaz de usuario](ui-automation-control-types-overview.md)
- [Información general sobre la Automatización de la interfaz de usuario](ui-automation-overview.md)
