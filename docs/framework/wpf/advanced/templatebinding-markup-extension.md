---
title: Extensión de marcado TemplateBinding
ms.date: 03/30/2017
f1_keywords:
- TemplateBinding
- TemplateBindingExtension
helpviewer_keywords:
- XAML [WPF], TemplateBinding markup extension
- TemplateBinding markup extensions [WPF]
ms.assetid: 1d25bbfc-dbc2-499d-9f12-419d23d4ac6a
ms.openlocfilehash: 399e4ac223d2fcb728ece2c92d25a087990992f2
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2019
ms.locfileid: "73458669"
---
# <a name="templatebinding-markup-extension"></a>Extensión de marcado TemplateBinding
Vincula el valor de una propiedad de una plantilla de control para que sea el valor de otra propiedad del control con plantilla.  
  
## <a name="xaml-attribute-usage"></a>Uso de atributos XAML  
  
```xml  
<object property="{TemplateBinding sourceProperty}" .../>  
```  
  
## <a name="xaml-attribute-usage-for-setter-property-in-template-or-style"></a>Uso de atributos XAML (para la propiedad Setter de una plantilla o estilo)  
  
```xml  
<Setter Property="propertyName" Value="{TemplateBinding sourceProperty}" .../>  
```  
  
## <a name="xaml-values"></a>Valores XAML  
  
|||  
|-|-|  
|`propertyName`|Propiedad <xref:System.Windows.DependencyProperty.Name%2A?displayProperty=nameWithType> que se va establecer en la sintaxis del establecedor.|  
|`sourceProperty`|Otra propiedad de dependencia existente en el tipo con plantilla, especificada por el valor de <xref:System.Windows.DependencyProperty.Name%2A?displayProperty=nameWithType>.<br /><br /> O bien<br /><br /> Nombre de propiedad "relacionada" que se define por un tipo diferente del tipo de destino que se va a convertir en un tipo con plantilla. En realidad, se trata de un objeto <xref:System.Windows.PropertyPath>. Consulte [sintaxis XAML de PropertyPath](propertypath-xaml-syntax.md).|  
  
## <a name="remarks"></a>Comentarios  
 Un `TemplateBinding` es una forma optimizada de un [enlace](binding-markup-extension.md) para escenarios de plantilla, similar a un `Binding` construido con `{Binding RelativeSource={RelativeSource TemplatedParent}}`. `TemplateBinding` siempre es un enlace unidireccional, aunque las propiedades implicadas establezcan por defecto un enlace bidireccional. Ambas propiedades implicadas deben ser propiedades de dependencia. Para lograr el enlace bidireccional a un elemento primario con plantilla, use en su lugar la siguiente instrucción de enlace `{Binding RelativeSource={RelativeSource TemplatedParent}, Mode=TwoWay, Path=MyDependencyProperty}`. 
  
 [RelativeSource](relativesource-markupextension.md) es otra extensión de marcado que a veces se usa junto con o en lugar de `TemplateBinding` para realizar un enlace de propiedad relativo dentro de una plantilla.  
  
 La descripción de las plantillas de control como concepto no se trata aquí. para obtener más información, vea [estilos y plantillas de control](../controls/control-styles-and-templates.md).  
  
 La sintaxis de atributo es la que se usa normalmente con esta extensión de marcado. El token de cadena que se proporciona después de la cadena de identificador `TemplateBinding` se asigna como valor de <xref:System.Windows.TemplateBindingExtension.Property%2A> de la clase de extensión <xref:System.Windows.TemplateBindingExtension> subyacente.  
  
 La sintaxis de elementos de objeto es posible, pero no se muestra porque no tiene ninguna aplicación en el mundo real. `TemplateBinding` se emplea para rellenar los valores dentro de los establecedores, mediante expresiones evaluadas, y el uso de la sintaxis de elementos de objeto para que `TemplateBinding` rellene la sintaxis de elementos de propiedad de `<Setter.Property>` aplica un grado de detalle innecesario.  
  
 `TemplateBinding` también se puede utilizar en el uso de atributos detallado que especifica la propiedad <xref:System.Windows.TemplateBindingExtension.Property%2A> como un par de propiedad=valor:  
  
```xml  
<object property="{TemplateBinding Property=sourceProperty}" .../>  
```  
  
 El uso detallado suele ser útil para las extensiones que tienen más de una propiedad que se puede configurar, o en aquellos casos en que algunas propiedades son opcionales. Dado que `TemplateBinding` tiene una sola propiedad configurable, que es obligatoria, este uso detallado no es habitual.  
  
 En la implementación del procesador de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] XAML, el control de esta extensión de marcado se define mediante la clase <xref:System.Windows.TemplateBindingExtension>.  
  
 `TemplateBinding` es una extensión de marcado. Las extensiones de marcado se suelen implementar cuando se necesita que los valores de los atributos de escape no sean valores literales o nombres de controladores, y este requisito es de índole más global que limitarse a colocar los convertidores de tipos en determinados tipos o propiedades. Todas las extensiones de marcado de XAML usan los caracteres `{` y `}` en su sintaxis de atributo, que es la Convención por la que un procesador XAML reconoce que una extensión de marcado debe procesar el atributo. Para más información, vea [Extensiones de marcado y XAML de WPF](markup-extensions-and-wpf-xaml.md).  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Style>
- <xref:System.Windows.Controls.ControlTemplate>
- [Aplicar estilos y plantillas](../controls/styling-and-templating.md)
- [Información general sobre XAML (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [Extensiones de marcado y XAML de WPF](markup-extensions-and-wpf-xaml.md)
- [RelativeSource (extensión de marcado)](relativesource-markupextension.md)
- [Binding (extensión de marcado)](binding-markup-extension.md)
