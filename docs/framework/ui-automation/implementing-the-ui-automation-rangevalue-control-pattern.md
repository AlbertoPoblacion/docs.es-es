---
title: Implementar el patrón de control RangeValue de UI Automation
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Range Value
- Range Value control pattern
- UI Automation, Range Value control pattern
ms.assetid: 225feaa4-918e-418b-938e-7389338d0a69
ms.openlocfilehash: aeb14bddf98adf53a52c8897994bd0fb6fa498ad
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59175804"
---
# <a name="implementing-the-ui-automation-rangevalue-control-pattern"></a>Implementar el patrón de control RangeValue de UI Automation
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener información más reciente sobre [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: Automatización de interfaz de usuario](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 En este tema se presentan las directrices y convenciones para implementar <xref:System.Windows.Automation.Provider.IRangeValueProvider>, incluida la información sobre eventos y propiedades. Al final del tema se ofrecen vínculos a referencias adicionales.  
  
 El patrón de control <xref:System.Windows.Automation.RangeValuePattern> se utiliza para admitir controles que se pueden establecer en un valor dentro de un intervalo. Para obtener ejemplos de controles que implementan este patrón de control, vea [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>Directrices y convenciones de implementación  
 Al implementar el patrón de control Range Value, tenga en cuenta las siguientes directrices y convenciones:  
  
-   Los controles permiten la recalibración de sus propiedades compatibles según las preferencias de usuario o la configuración regional. Un ejemplo de esto es un control de termómetro que puede establecerse para mostrar la temperatura en grados Fahrenheit o Celsius.  
  
-   Los controles que tienen valores de intervalo ambiguos, como las barras de progreso o los controles deslizantes, deben tener dichos valores normalizados.  
  
 ![Barra de progreso. ](../../../docs/framework/ui-automation/media/uia-rangevaluepattern-progress-bar.PNG "UIA_RangeValuePattern_Progress_Bar")  
Ejemplo de una barra de progreso donde el valor es de tipo entero y los valores de propiedad mínimo y máximo se normalizan en 0 y 100, respectivamente  
  
<a name="Required_Members_for_the_IRangeValueProvider"></a>   
## <a name="required-members-for-irangevalueprovider"></a>Miembros requeridos para IRangeValueProvider  
  
|Miembro requerido|Tipo de miembro|Notas|  
|---------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.RangeValuePattern.IsReadOnlyProperty>|Propiedad|Ninguna|  
|<xref:System.Windows.Automation.RangeValuePattern.ValueProperty>|Propiedad|Ninguna|  
|<xref:System.Windows.Automation.RangeValuePattern.LargeChangeProperty>|Propiedad|Ninguna|  
|<xref:System.Windows.Automation.RangeValuePattern.SmallChangeProperty>|Propiedad|Ninguna|  
|<xref:System.Windows.Automation.RangeValuePattern.MaximumProperty>|Propiedad|Ninguna|  
|<xref:System.Windows.Automation.RangeValuePattern.MinimumProperty>|Propiedad|Ninguna|  
|<xref:System.Windows.Automation.RangeValuePattern.SetValue%2A>|Métodos|Ninguna|  
  
 Este patrón de control no tiene eventos asociados.  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>Excepciones  
 Los proveedores deben producir las siguientes excepciones.  
  
|Tipo de excepción|Condición|  
|--------------------|---------------|  
|<xref:System.ArgumentOutOfRangeException>|Se llama a<xref:System.Windows.Automation.RangeValuePattern.SetValue%2A> con un valor que es mayor que <xref:System.Windows.Automation.RangeValuePattern.MaximumProperty> o menor que <xref:System.Windows.Automation.RangeValuePattern.MinimumProperty>.|  
  
## <a name="see-also"></a>Vea también

- [Información general sobre los patrones de control de la Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)
- [Patrones de control compatibles en un proveedor de Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)
- [Patrones de control de Automatización de la interfaz de usuario para clientes](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)
- [Información general sobre el árbol de la Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)
- [Uso del almacenamiento en caché en la Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)
