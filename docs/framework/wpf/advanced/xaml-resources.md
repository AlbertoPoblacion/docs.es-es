---
title: Recursos XAML
ms.date: 03/30/2017
helpviewer_keywords:
- reusing resources [WPF]
- resources [WPF], reusing
- reusing commonly defined objects [WPF]
- XAML [WPF], reusing resources
ms.assetid: 91580b89-a0a8-4889-aecb-fddf8e63175f
ms.openlocfilehash: 0176ebffe82e60671ea66481b7d659004dc31477
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757084"
---
# <a name="xaml-resources"></a>Recursos XAML
Un recurso es un objeto que se puede volver a usar en diferentes sitios de la aplicación. Pinceles y estilos son ejemplos de recursos. Esta introducción describe cómo usar los recursos de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. También puede crear y tener acceso a recursos mediante código o indistintamente entre código y [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]. Para obtener más información, consulte [recursos y código](resources-and-code.md).  
  
> [!NOTE]
>  Los archivos de recursos que se describe en este tema son diferentes de los archivos de recursos se describen en [WPF Application Resource, contenido y los archivos de datos](../app-development/wpf-application-resource-content-and-data-files.md) y diferentes de los recursos incrustados o vinculados que se describe en [administrar Recursos de la aplicación (. NET)](/visualstudio/ide/managing-application-resources-dotnet).  

<a name="usingresources"></a>   
## <a name="using-resources-in-xaml"></a>Uso de recursos en XAML  
 En el ejemplo siguiente se define un <xref:System.Windows.Media.SolidColorBrush> como un recurso en el elemento raíz de una página. En el ejemplo, a continuación, hace referencia al recurso y lo usa para establecer las propiedades de varios elementos secundarios, incluida una <xref:System.Windows.Shapes.Ellipse>, un <xref:System.Windows.Controls.TextBlock>y un <xref:System.Windows.Controls.Button>.  
  
 [!code-xaml[FEResourceSH_snip#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xaml)]  
  
 Cada elemento de nivel de marco (<xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>) tiene un <xref:System.Windows.FrameworkElement.Resources%2A> propiedad, que es la propiedad que contiene los recursos (como un <xref:System.Windows.ResourceDictionary>) que define un recurso. Puede definir recursos en cualquier elemento. Sin embargo, los recursos se definen con más frecuencia en el elemento raíz, que es <xref:System.Windows.Controls.Page> en el ejemplo.  
  
 Cada recurso en un diccionario de recursos debe tener una clave única. Al definir los recursos en el marcado, asigna la clave única a través de la [Directiva x: Key](../../xaml-services/x-key-directive.md). Normalmente, la clave es una cadena; pero puede también establecerla para otros tipos de objetos usando las extensiones de marcado apropiadas. Las claves que no son cadenas de recursos se usan por ciertas áreas de características de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], en particular para los estilos, los recursos del componente y los estilos de datos.  
  
 Después de definir un recurso, puede hacer referencia a los recursos que se usarán para un valor de propiedad mediante una sintaxis de extensión de marcado de recursos que especifica el nombre de clave, por ejemplo:  
  
 [!code-xaml[FEResourceSH_snip#KeyNameUsage](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#keynameusage)]  
  
 En el ejemplo anterior, cuando el [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] cargador procesa el valor `{StaticResource MyBrush}` para el <xref:System.Windows.Controls.Control.Background%2A> propiedad <xref:System.Windows.Controls.Button>, la lógica de búsqueda de recursos comprueba en primer lugar el diccionario de recursos para el <xref:System.Windows.Controls.Button> elemento. Si <xref:System.Windows.Controls.Button> no tiene una definición de la clave de recurso `MyBrush` (no la tiene; su colección de recursos está vacía), a continuación, la búsqueda comprueba el elemento primario del <xref:System.Windows.Controls.Button>, que es <xref:System.Windows.Controls.Page>. Por lo tanto, al definir un recurso en el <xref:System.Windows.Controls.Page> elemento raíz, todos los elementos en el árbol lógico de la <xref:System.Windows.Controls.Page> puede tener acceso a él y puede reutilizar el mismo recurso para establecer el valor de cualquier propiedad que acepta el <xref:System.Type> que el recurso representa. En el ejemplo anterior, el mismo `MyBrush` dos propiedades diferentes conjuntos de recursos: la <xref:System.Windows.Controls.Control.Background%2A> de un <xref:System.Windows.Controls.Button>y el <xref:System.Windows.Shapes.Shape.Fill%2A> de un <xref:System.Windows.Shapes.Rectangle>.  
  
<a name="staticdynamic"></a>   
## <a name="static-and-dynamic-resources"></a>Recursos estáticos y dinámicos  
 Puede hacer referencia a un recurso como un recurso estático o un recurso dinámico. Esto se hace mediante el uso del [StaticResource Markup Extension](staticresource-markup-extension.md) o [DynamicResource Markup Extension](dynamicresource-markup-extension.md). Una extensión de marcado es una característica de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] según la cual puede especificar una referencia de objeto al tener la extensión de marcado de procesar la cadena de atributo y devolver el objeto a un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] cargador. Para obtener más información sobre el comportamiento de la extensión de marcado, consulte [extensiones de marcado y WPF XAML](markup-extensions-and-wpf-xaml.md).  
  
 Cuando se usa una extensión de marcado, normalmente proporciona uno o varios parámetros en forma de cadena que son procesados por dicha extensión de marcado, en lugar de que se evalúe en el contexto de la propiedad que se va a establecer. El [StaticResource Markup Extension](staticresource-markup-extension.md) procesa una clave buscando el valor para esa clave en todos los diccionarios de recursos disponibles. Esto sucede durante la carga, que es el punto en el tiempo cuando el proceso de carga necesita asignar el valor de propiedad que acepta la referencia de recurso estático. El [DynamicResource Markup Extension](dynamicresource-markup-extension.md) en su lugar los procesos de una clave mediante la creación de una expresión y dicha expresión permanece sin evaluar hasta que realmente se ejecuta la aplicación, momento en el que se evalúa la expresión y proporciona un valor.  
  
 Al hacer referencia a un recurso, independientemente de si usa una referencia de recurso estático o una referencia de recurso dinámico, pueden influir las siguientes consideraciones:  
  
- El diseño general de cómo crear los recursos de la aplicación (por página, en la aplicación, sueltos en [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], en un ensamblado solo de recursos).  
  
- La función de la aplicación: ¿la actualización de recursos en tiempo real forma parte de los requisitos de la aplicación?  
  
- El comportamiento de búsqueda respectivo de ese tipo de referencia de recurso.  
  
- La propiedad o tipo de recurso determinado y el comportamiento nativo de esos tipos.  
  
### <a name="static-resources"></a>Recursos estáticos  
 Las referencias de recursos estáticos trabajan mejor en las siguientes circunstancias:  
  
- El diseño de la aplicación concentra la mayoría de todos sus recursos en la página o en los diccionarios de recursos en el nivel de aplicación. Las referencias de recursos estáticos no se vuelven a evaluar en función de comportamientos en tiempo de ejecución, como recargar una página y, por tanto, puede haber algunas ventajas de rendimiento para evitar grandes cantidades de referencias de recursos dinámicos cuando no son necesarios por su diseño de aplicaciones y recursos.  
  
- Se establece el valor de una propiedad que no se encuentra en un <xref:System.Windows.DependencyObject> o <xref:System.Windows.Freezable>.  
  
- Está creando un diccionario de recursos que se compilará en un archivo DLL y que se empaqueta como parte de la aplicación o se comparte entre aplicaciones.  
  
- Está creando un tema para un control personalizado y está definiendo recursos que se usan dentro de los temas. En este caso, normalmente no quiere el comportamiento de búsqueda de referencia de recursos dinámicos, sino el comportamiento de referencia de recursos estáticos, de manera que la búsqueda sea predecible e independiente para el tema. Con una referencia de recursos dinámicos, incluso una referencia dentro de un tema se deja sin evaluar hasta el tiempo de ejecución y es probable que, cuando se aplica el tema, algún elemento local vuelva a definir una clave a la que el tema está intentando hacer referencia, y el elemento local se detectará antes que el propio tema en la búsqueda. Si esto sucede, el tema no se comportará de la manera esperada.  
  
- Está usando recursos para establecer grandes cantidades de propiedades de dependencia. Las propiedades de dependencia tienen un almacenamiento en caché de valores efectivos habilitado por el sistema de propiedades, así que si proporciona un valor para una propiedad de dependencia que pueda evaluarse en tiempo de carga, la propiedad de dependencia no tiene que comprobar una expresión que se ha vuelto a evaluar y puede devolver el último valor efectivo. Esta técnica puede suponer una ventaja de rendimiento.  
  
- Para cambiar el recurso subyacente para todos los consumidores o quiere mantener instancias grabables independientes para cada consumidor mediante el uso de la [x: Shared Attribute](../../xaml-services/x-shared-attribute.md).  
  
#### <a name="static-resource-lookup-behavior"></a>Comportamiento de búsqueda de recursos estáticos  
  
1. El proceso de búsqueda comprueba la clave solicitada en el diccionario de recursos que ha definido el elemento que establece la propiedad.  
  
2. Después, el proceso de búsqueda recorre el árbol lógico hacia arriba, hasta el elemento primario y su diccionario de recursos. Esto continúa hasta que se alcanza el elemento raíz.  
  
3. Después, se comprueban los recursos de la aplicación. Recursos de la aplicación son aquellos recursos dentro del diccionario de recursos definido por el <xref:System.Windows.Application> objeto para su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicación.  
  
 Las referencias de recursos estáticos del interior de un diccionario de recursos deben hacer referencia a un recurso que ya se haya definido léxicamente antes que la referencia de recurso. No se pueden resolver las referencias adelantadas mediante una referencia de recursos estáticos. Por este motivo, si usa referencias de recursos estáticos, debe diseñar la estructura del diccionario de recursos de manera que los recursos previstos para su uso mediante recurso se definan en o cerca del principio de cada diccionario de recursos respectivo.  
  
 Puede ampliar la búsqueda de recursos estáticos a los temas, o a los recursos del sistema, pero esto solo se admite porque el [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] aplaza el cargador de la solicitud. El aplazamiento es necesario, de manera que el tema en tiempo de ejecución en el momento de la carga de la página se aplique correctamente en la aplicación. En cambio, no se recomiendan las referencias de recursos estáticos a las claves que se sabe que solo existen en temas o como recursos del sistema. Esto se debe a que dichas referencias no se vuelven a evaluar si el usuario modifica el tema en tiempo real. Una referencia de recurso dinámico es más confiable cuando solicita un tema o recursos del sistema. La excepción se produce cuando un elemento de tema solicita otro recurso. Estas referencias deben ser referencias de recursos estáticos, por los motivos que se han mencionado anteriormente.  
  
 El comportamiento de excepción si no se detecta una referencia de recursos estáticos varía. Si el recurso se ha aplazado, entonces la excepción se produce en tiempo de ejecución. Si el recurso no se ha aplazado, la excepción se produce en tiempo de carga.  
  
### <a name="dynamic-resources"></a>Recursos dinámicos  
 Los recursos dinámicos trabajan mejor en las siguientes circunstancias:  
  
- El valor del recurso depende de las condiciones que no se conocen hasta el tiempo de ejecución. Esto incluye los recursos del sistema o recursos que, de otro modo, son configurables por el usuario. Por ejemplo, puede crear valores de establecedor que hacen referencia a propiedades del sistema, tal como se expone por <xref:System.Windows.SystemColors>, <xref:System.Windows.SystemFonts>, o <xref:System.Windows.SystemParameters>. Estos valores son verdaderamente dinámicos porque proceden en definitiva del entorno en tiempo de ejecución del usuario y del sistema operativo. También puede tener temas en el nivel de aplicación que pueden cambiar, donde el acceso a los recursos de nivel de página también debe capturar el cambio.  
  
- Está creando o haciendo referencia a estilos del tema para un control personalizado.  
  
- Pretende ajustar el contenido de un <xref:System.Windows.ResourceDictionary> durante un período de duración de la aplicación.  
  
- Tiene una estructura de recursos complicada que tiene interdependencias, donde puede necesitarse una referencia adelantada. Referencias de recursos estáticos no admiten las referencias adelantadas, pero las referencias de recursos dinámicos sí lo admiten porque no es necesario que el recurso se puede evaluar hasta el tiempo de ejecución y las referencias adelantadas, por tanto, no son un concepto relevante.  
  
- Está haciendo referencia a un recursos que es especialmente grande desde la perspectiva de una compilación o espacio de trabajo, y el recurso puede no usarse inmediatamente cuando se carga la página. Referencias de recursos estáticos siempre se cargan desde [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] cuando se cargue la página; sin embargo, una referencia de recurso dinámico no se carga hasta que se usa realmente.  
  
- Está creando un estilo donde los valores del establecedor pueden provenir de otros valores que están influenciados por temas u otra configuración del usuario.  
  
- Está aplicando recursos en elementos en los que se puede cambiar el elemento primario en el árbol lógico durante la vigencia de la aplicación. Cambiar el elemento primario también cambia potencialmente el ámbito de búsqueda de recursos, por lo que si quiere que el recurso de un elemento primario que se puede cambiar se vuelva a evaluar basándose en el nuevo ámbito, use siempre una referencia de recurso dinámico.  
  
#### <a name="dynamic-resource-lookup-behavior"></a>Comportamiento de búsqueda de recursos dinámicos  
 Comportamiento de búsqueda de recursos de una referencia de recurso dinámico es similar al comportamiento de búsqueda en el código si llama a <xref:System.Windows.FrameworkElement.FindResource%2A> o <xref:System.Windows.FrameworkElement.SetResourceReference%2A>.  
  
1. El proceso de búsqueda comprueba la clave solicitada en el diccionario de recursos que ha definido el elemento que establece la propiedad.  
  
    - Si el elemento define un <xref:System.Windows.FrameworkElement.Style%2A> propiedad, el <xref:System.Windows.Style.Resources%2A> diccionario dentro de la <xref:System.Windows.Style> está activada.  
  
    - Si el elemento define un <xref:System.Windows.Controls.Control.Template%2A> propiedad, el <xref:System.Windows.FrameworkTemplate.Resources%2A> diccionario dentro de la <xref:System.Windows.FrameworkTemplate> está activada.  
  
2. Después, el proceso de búsqueda recorre el árbol lógico hacia arriba, hasta el elemento primario y su diccionario de recursos. Esto continúa hasta que se alcanza el elemento raíz.  
  
3. Después, se comprueban los recursos de la aplicación. Recursos de la aplicación son aquellos recursos dentro del diccionario de recursos definido por el <xref:System.Windows.Application> objeto para su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicación.  
  
4. Se comprueba el diccionario de recursos de temas para el tema activo actualmente. Si el tema cambia en tiempo de ejecución, el valor se vuelve a evaluar.  
  
5. Se comprueban los recursos del sistema.  
  
 El comportamiento de excepción (si existe) varía:  
  
- Si se ha solicitado un recurso mediante un <xref:System.Windows.FrameworkElement.FindResource%2A> llamar y no se encontró, se produce una excepción.  
  
- Si se ha solicitado un recurso mediante un <xref:System.Windows.FrameworkElement.TryFindResource%2A> llamar y no se encontró, no se genera ninguna excepción, pero el valor devuelto es `null`. Si la propiedad que se va a establecer no acepta `null`, a continuación, sigue siendo posible que se producirá una excepción más profunda (Esto depende de la propiedad individual que se va a establecer).  
  
- Si se ha solicitado un recurso mediante una referencia de recurso dinámico en [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]y no se encontró, a continuación, el comportamiento depende del sistema de propiedades general, pero el comportamiento general es como si se ha producido ninguna operación de configuración de la propiedad en el nivel donde existe el recurso. Por ejemplo, si intenta establecer el fondo en un elemento de botón individual con un recurso que no puede evaluarse, entonces no se establece ningún valor, pero el valor efectivo todavía puede provenir de otros participantes del sistema de propiedades y la precedencia de valores. Por ejemplo, el valor de fondo todavía puede provenir de un estilo de botón definido localmente, o desde el estilo del tema. Para las propiedades que no se definen mediante los estilos del tema, el valor efectivo después de una evaluación de recursos incorrecta puede provenir del valor predeterminado de los metadatos de la propiedad.  
  
#### <a name="restrictions"></a>Restricciones  
 Las referencias de recursos dinámicos tienen algunas restricciones importantes. Debe cumplirse al menos una de las siguientes:  
  
- La propiedad se establezca debe ser una propiedad en un <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement>. Que la propiedad debe estar respaldada por un <xref:System.Windows.DependencyProperty>.  
  
- La referencia es para un valor dentro de un <xref:System.Windows.Style> <xref:System.Windows.Setter>.  
  
- La propiedad se establezca debe ser una propiedad en un <xref:System.Windows.Freezable> que se proporciona como un valor de uno de ellos un <xref:System.Windows.FrameworkElement> o <xref:System.Windows.FrameworkContentElement> propiedad, o un <xref:System.Windows.Setter> valor.  
  
 Dado que la propiedad que se establece debe ser un <xref:System.Windows.DependencyProperty> o <xref:System.Windows.Freezable> propiedad, pueden propagar la mayoría de los cambios de propiedad a la interfaz de usuario porque se confirma un cambio de propiedad (el valor de recurso dinámico modificado) por el sistema de propiedades. Mayoría de los controles incluye lógica que forzará otro diseño de un control si un <xref:System.Windows.DependencyProperty> los cambios y que propiedad puede afectar al diseño. Sin embargo, no todas las propiedades que tienen un [DynamicResource Markup Extension](dynamicresource-markup-extension.md) como su valor se garantiza que proporcione el valor de tal manera que actualizan en tiempo real en la interfaz de usuario. Esa función todavía puede variar dependiendo de la propiedad, así como dependiendo del tipo que posea la propiedad, o incluso de la estructura lógica de la aplicación.  
  
<a name="stylesimplicitkeys"></a>   
## <a name="styles-datatemplates-and-implicit-keys"></a>Estilos, plantillas de datos y claves implícitas  
 Anteriormente, se ha mencionado que todos los elementos de un <xref:System.Windows.ResourceDictionary> debe tener una clave. Sin embargo, eso no significa que todos los recursos deben tener una explícita `x:Key`. Varios tipos de objetos admiten una clave implícita cuando se definen como un recurso, donde el valor de clave está vinculado al valor de otra propiedad. Esto se conoce como una clave implícita, mientras que un `x:Key` atributo es una clave explícita. Puede sobrescribir cualquier clave implícita especificando una clave explícita.  
  
 Un escenario muy importante para los recursos consiste en definir un <xref:System.Windows.Style>. De hecho, un <xref:System.Windows.Style> casi siempre se define como una entrada en un diccionario de recursos, porque los estilos están previstos para su reutilización. Para obtener más información sobre los estilos, consulte [aplicar estilos y plantillas](../controls/styling-and-templating.md).  
  
 Los estilos para los controles pueden crearse y hacerse referencia con una clave implícita. Los estilos de tema que definen la apariencia predeterminada de un control se basan en esta clave implícita. La clave implícita desde el punto de vista de su solicitud es el <xref:System.Type> del propio control. La clave implícita desde el punto de vista de definir el recurso es el <xref:System.Windows.Style.TargetType%2A> del estilo. Por lo tanto, si está creando temas para controles personalizados, creando estilos que interactúen con los estilos de tema existente, no necesitará especificar un [Directiva x: Key](../../xaml-services/x-key-directive.md) para que <xref:System.Windows.Style>. Y si quiere usar los estilos temáticos, no necesita especificar ningún estilo. Por ejemplo, la siguiente definición de estilo funciona, aunque el <xref:System.Windows.Style> recursos no parecen tener una clave:  
  
 [!code-xaml[FEResourceSH_snip#ImplicitStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#implicitstyle)]  
  
 Que estilo realmente tiene una clave: la clave implícita `typeof(` <xref:System.Windows.Controls.Button> `)`. En el marcado, puede especificar un <xref:System.Windows.Style.TargetType%2A> directamente como el tipo de nombre (o también puede usar [{x: Type...}](../../xaml-services/x-type-markup-extension.md) para devolver un <xref:System.Type>.  
  
 Mediante los mecanismos de estilo de tema predeterminado utilizados por [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], ese estilo se aplica como el estilo en tiempo de ejecución de un <xref:System.Windows.Controls.Button> en la página, incluso aunque el <xref:System.Windows.Controls.Button> propio no intenta especificar su <xref:System.Windows.FrameworkElement.Style%2A> propiedad o un recurso específico hacer referencia al estilo. Su estilo definido en la página se encuentra anteriormente en la secuencia de búsqueda que el estilo del diccionario de tema con la misma clave que tiene el estilo del diccionario de tema. Simplemente puede especificar `<Button>Hello</Button>` en cualquier parte de la página y el estilo definido con <xref:System.Windows.Style.TargetType%2A> de `Button` se aplicaría a ese botón. Si lo desea, puede clave explícitamente el estilo con el mismo valor de tipo como <xref:System.Windows.Style.TargetType%2A>, para mayor claridad en el marcado, pero que es opcional.  
  
 Las claves implícitas para los estilos no se aplican en un control si <xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A> es `true` (tenga en cuenta también que <xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A> puede establecerse como parte del comportamiento nativo para la clase de control, en lugar de forma explícita en una instancia del control). Además, para admitir claves implícitas para los escenarios de la clase derivada, el control debe invalidar <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> (todos los controles existentes que se proporciona como parte de [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] hacerlo). Para obtener más información acerca de los estilos, temas y diseño de control, vea [directrices para diseñar controles con estilos](../controls/guidelines-for-designing-stylable-controls.md).  
  
 <xref:System.Windows.DataTemplate> También tiene una clave implícita. La clave implícita de un <xref:System.Windows.DataTemplate> es la <xref:System.Windows.DataTemplate.DataType%2A> valor de propiedad. <xref:System.Windows.DataTemplate.DataType%2A> También se puede especificar como el nombre del tipo en lugar de forma explícita mediante [{x: Type...} ](../../xaml-services/x-type-markup-extension.md). Para obtener más información, consulte [Data Templating Overview](../data/data-templating-overview.md).  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.ResourceDictionary>
- [Recursos de la aplicación](optimizing-performance-application-resources.md)
- [Recursos y código](resources-and-code.md)
- [Definir y hacer referencia a un recurso](how-to-define-and-reference-a-resource.md)
- [Información general sobre la administración de aplicaciones](../app-development/application-management-overview.md)
- [x:Type (extensión de marcado)](../../xaml-services/x-type-markup-extension.md)
- [StaticResource (extensión de marcado)](staticresource-markup-extension.md)
- [DynamicResource (extensión de marcado)](dynamicresource-markup-extension.md)
