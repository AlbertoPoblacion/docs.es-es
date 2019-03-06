---
title: Información general sobre declaraciones de enlaces
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- markup extensions [WPF]
- data binding [WPF], declarations
- object element syntax [WPF]
- binding data [WPF], declarations
- syntax [WPF], object elements
- binding declarations [WPF]
ms.assetid: b97fd626-4c0d-4761-872a-2bca5820da2c
ms.openlocfilehash: 2ef632ee1335d1ee0e94eaa1a7f25cbe34ed4e6f
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2019
ms.locfileid: "57363431"
---
# <a name="binding-declarations-overview"></a>Información general sobre declaraciones de enlaces
En este tema se describen las distintas formas de declarar un enlace.  
  
 
  
<a name="Prereq"></a>   
## <a name="prerequisites"></a>Requisitos previos  
 Antes de leer este tema, es importante que esté familiarizado con el concepto y el uso de las extensiones de marcado. Para más información sobre las extensiones de marcado, consulte [Extensiones de marcado y XAML de WPF](../advanced/markup-extensions-and-wpf-xaml.md).  
  
 En este tema no se tratan los conceptos de enlace de datos. Para obtener una explicación de los conceptos de enlace de datos, consulte [Información general sobre el enlace de datos](data-binding-overview.md).  
  
<a name="BindinginXAML"></a>   
## <a name="declaring-a-binding-in-xaml"></a>Declarar un enlace en XAML  
 En esta sección se describe cómo declarar en XAML.  
  
<a name="MarkupExtensionSyntax"></a>   
### <a name="markup-extension-usage"></a>Uso de la extensión de marcado  
 <xref:System.Windows.Data.Binding> es una extensión de marcado. Cuando se utiliza la extensión de enlace para declarar un enlace, la declaración consta de una serie de cláusulas después de la palabra clave `Binding` y separadas por comas (,). Las cláusulas de la declaración de enlace pueden estar en cualquier orden y hay muchas combinaciones posibles. Las cláusulas son *nombre*=*valor* pares where *nombre* es el nombre de la <xref:System.Windows.Data.Binding> propiedad y *valor* es el valor que se establece para la propiedad.  
  
 Al crear cadenas de declaración de enlace en el marcado, se adjuntará a la propiedad de dependencia concreta de un objeto de destino. El ejemplo siguiente muestra cómo enlazar la <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> propiedad mediante la extensión de enlace, especificando el <xref:System.Windows.Data.Binding.Source%2A> y <xref:System.Windows.Data.Binding.Path%2A> propiedades.  
  
 [!code-xaml[SimpleBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#L37-L37)]  
  
 Puede especificar la mayoría de las propiedades de la <xref:System.Windows.Data.Binding> esta forma de clase. Para obtener más información acerca de la extensión de enlace, así como una lista de <xref:System.Windows.Data.Binding> las propiedades que no se puede establecer mediante la extensión de enlace, consulte el [extensión de marcado de enlace](../advanced/binding-markup-extension.md) información general.  
  
<a name="ObjectElementSyntax"></a>   
### <a name="object-element-syntax"></a>Sintaxis de elemento de objeto  
 La sintaxis de elemento de objeto es una alternativa a la creación de la declaración de enlace. En la mayoría de los casos, no hay ninguna ventaja particular para usar la extensión de marcado o la sintaxis de elemento de objeto. Sin embargo, en aquellos casos en los que la extensión de marcado no admite el escenario, como cuando el valor de la propiedad es de un tipo que no es una cadena para la que no existe conversión de tipo, debe utilizar la sintaxis de elemento de objeto.  
  
 El siguiente es un ejemplo de la sintaxis de elemento de objeto y el uso de la extensión de marcado:  
  
 [!code-xaml[BindConversionMarkup#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversionMarkup/CSharp/Page1.xaml#1)]  
  
 El ejemplo se enlaza el <xref:System.Windows.Controls.TextBlock.Foreground%2A> propiedad declarando un enlace mediante la sintaxis de extensión. La declaración de enlace para el <xref:System.Windows.Controls.TextBlock.Text%2A> propiedad utiliza la sintaxis de elemento de objeto.  
  
 Para más información sobre los distintos términos, consulte [Detalles de la sintaxis XAML](../advanced/xaml-syntax-in-detail.md).  
  
<a name="MBandPB"></a>   
### <a name="multibinding-and-prioritybinding"></a>MultiBinding y PriorityBinding  
 <xref:System.Windows.Data.MultiBinding> y <xref:System.Windows.Data.PriorityBinding> no admiten la sintaxis de extensión XAML. Por lo tanto, debe usar la sintaxis de elemento de objeto si declara un <xref:System.Windows.Data.MultiBinding> o <xref:System.Windows.Data.PriorityBinding> en XAML.  
  
<a name="BindinginCode"></a>   
## <a name="creating-a-binding-in-code"></a>Crear un enlace mediante código  
 Otra manera de especificar un enlace consiste en establecer las propiedades directamente en un <xref:System.Windows.Data.Binding> objeto en el código. El ejemplo siguiente muestra cómo crear un <xref:System.Windows.Data.Binding> de objetos y especificar las propiedades en el código.  En este ejemplo, `TheConverter` es un objeto que implementa el <xref:System.Windows.Data.IValueConverter> interfaz.  
  
 [!code-csharp[BindConversion#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#1)]
 [!code-vb[BindConversion#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#1)]  
  
 Si el objeto que se va a enlazar es un <xref:System.Windows.FrameworkElement> o un <xref:System.Windows.FrameworkContentElement> puede llamar a la `SetBinding` método en el objeto directamente en lugar de usar <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=nameWithType>. Para obtener un ejemplo, consulte [Crear un enlace mediante código](how-to-create-a-binding-in-code.md).  
  
<a name="Path_Syntax"></a>   
## <a name="binding-path-syntax"></a>Sintaxis de la ruta de enlace  
 Use el <xref:System.Windows.Data.Binding.Path%2A> propiedad para especificar el valor de origen que desea enlazar:  
  
-   En el caso más simple, el <xref:System.Windows.Data.Binding.Path%2A> valor de propiedad es el nombre de la propiedad del objeto de origen que se usará para el enlace, tales como `Path=PropertyName`.  
  
-   Se pueden especificar subpropiedades de una propiedad mediante una sintaxis similar como en C#. Por ejemplo, la cláusula `Path=ShoppingCart.Order` define el enlace a la subpropiedad `Order` del objeto o la propiedad `ShoppingCart`.  
  
-   Para enlazar a una propiedad adjunta, coloque paréntesis alrededor de esta propiedad. Por ejemplo, para enlazar a la propiedad adjunta <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>, la sintaxis es `Path=(DockPanel.Dock)`.  
  
-   Los indizadores de una propiedad pueden especificarse entre corchetes después del nombre de la propiedad donde se aplica el indizador. Por ejemplo, la cláusula `Path=ShoppingCart[0]` establece el enlace al índice que se corresponde a cómo la indización interna de la propiedad administra la cadena literal "0". También se admiten indizadores anidados.  
  
-   Los indizadores y las subpropiedades se pueden combinar en una cláusula `Path`; por ejemplo, `Path=ShoppingCart.ShippingInfo[MailingAddress,Street].`.  
  
-   Dentro de los indizadores pueden tener varios parámetros de indizador separados por comas (,). El tipo de cada parámetro se puede especificar con paréntesis. Por ejemplo, puede tener `Path="[(sys:Int32)42,(sys:Int32)24]"`, donde `sys` se asigna a la `System` espacio de nombres.  
  
-   Cuando el origen es una vista de colección, se puede especificar el elemento actual con una barra diagonal (/). Por ejemplo, la cláusula `Path=/` establece el enlace al elemento actual en la vista. Cuando el origen es una colección, esta sintaxis especifica el elemento actual de la vista de colección predeterminada.  
  
-   Las barras diagonales y los nombres de propiedad se pueden combinar para recorrer las propiedades que son colecciones. Por ejemplo, `Path=/Offices/ManagerName` especifica el elemento actual de la colección de origen, que contiene un `Offices` propiedad que también es una colección. Su elemento actual es un objeto que contiene un `ManagerName` propiedad.  
  
-   Opcionalmente, una ruta de acceso de punto (.) puede utilizarse para enlazar con el origen actual. Por ejemplo, `Text="{Binding}"` es equivalente a `Text="{Binding Path=.}"`.  
  
### <a name="escaping-mechanism"></a>Mecanismo de escape  
  
-   Dentro de los indizadores ([ ]), el carácter de intercalación (^) realiza el escape del carácter siguiente.  
  
-   Si establece <xref:System.Windows.Data.Binding.Path%2A> en XAML, también deberá escape (mediante entidades XML) ciertos caracteres que son especiales para la definición del lenguaje XML:  
  
    -   Use `&` para realizar el escape del carácter "&".  
  
    -   Use `>` para realizar el escape de la etiqueta final ">".  
  
-   Además, si describe el enlace completo en un atributo mediante la sintaxis de extensión de marcado, deberá realizar el escape (con la barra diagonal inversa \\) de los caracteres que son especiales para el analizador de extensión de marcado [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]:  
  
    -   La barra diagonal inversa (\\) es el mismo carácter de escape.  
  
    -   El signo igual (=) separa el nombre de propiedad del valor de propiedad.  
  
    -   La coma (,) separa las propiedades.  
  
    -   La llave de cierre (}) es el final de una extensión de marcado.  
  
<a name="Default"></a>   
## <a name="default-behaviors"></a>Comportamientos predeterminados  
 El comportamiento predeterminado es el siguiente si no se especifica en la declaración.  
  
-   Se crea un convertidor predeterminado que intenta realizar una conversión de tipos entre el valor de origen de enlace y el valor de destino del enlace. Si no se puede realizar una conversión, el convertidor predeterminado devuelve `null`.  
  
-   Si no establece <xref:System.Windows.Data.Binding.ConverterCulture%2A>, el motor de enlace utiliza la `Language` propiedad del objeto de destino de enlace. En XAML, tiene como valor predeterminado "en-US" o hereda el valor de elemento raíz (o cualquier elemento) de la página, si se ha establecido explícitamente.  
  
-   Siempre y cuando el enlace ya tiene un contexto de datos (por ejemplo, el contexto de datos heredado procedente de un elemento primario) y cualquier elemento o colección devuelta por ese contexto es adecuado para el enlace sin necesidad de realizar más modificaciones de la ruta de acceso, un declaración de enlace no puede tener ninguna cláusulas en absoluto: `{Binding}` Esto suele ser la manera en que se especifica un enlace para aplicar estilos a datos, donde el enlace se actúa sobre una colección. Para más información, consulte la sección "Utilizar objetos completos como origen de enlace" en [Información general sobre orígenes de enlaces](binding-sources-overview.md).  
  
-   El valor predeterminado <xref:System.Windows.Data.Binding.Mode%2A> varía entre unidireccional y bidireccional, según la propiedad de dependencia que se está enlazando. Siempre puede declarar explícitamente el modo de enlace para asegurarse de que el enlace tiene el comportamiento deseado. En las propiedades de control general, puede modificar el usuario, como <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> y <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A?displayProperty=nameWithType>, valor predeterminado enlaces bidireccionales, mientras que la mayoría de las propiedades valor predeterminado enlaces unidireccionales.  
  
-   El valor predeterminado <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> valor varía entre <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> y <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> dependiendo de la propiedad de dependencia enlazada. El valor predeterminado de la mayoría de las propiedades de dependencia es <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>, mientras que la propiedad <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> tiene un valor predeterminado de <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus>.  
  
## <a name="see-also"></a>Vea también
- [Información general sobre el enlace de datos](data-binding-overview.md)
- [Temas "Cómo..."](data-binding-how-to-topics.md)
- [Enlace de datos](../advanced/optimizing-performance-data-binding.md)
- [Sintaxis de PropertyPath de XAML](../advanced/propertypath-xaml-syntax.md)
