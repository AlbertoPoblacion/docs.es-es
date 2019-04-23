---
title: Globalización de WPF
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], international user interface
- XAML [WPF], globalization
- international user interface [WPF], XAML
- globalization [WPF]
ms.assetid: 4571ccfe-8a60-4f06-9b37-7ac0b1c2d10f
ms.openlocfilehash: 9a08fdeaa3517b1483af3f9958ad2db1c64648b8
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59084172"
---
# <a name="globalization-for-wpf"></a>Globalización de WPF
En este tema se presenta cuestiones que debe tener en cuenta al escribir [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] aplicaciones para el mercado global. Los elementos de programación de globalización se definen en [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] en `System.Globalization`.

<a name="xaml_globalization"></a>
## <a name="xaml-globalization"></a>Globalización XAML
 [!INCLUDE[TLA#tla_xaml#initcap](../../../../includes/tlasharptla-xamlsharpinitcap-md.md)] se basa en [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] y aprovecha la compatibilidad de globalización que se definen en el [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] especificación. Las siguientes secciones describen algunas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] características que debe tener en cuenta.

<a name="char_reference"></a>
### <a name="character-references"></a>Referencias de caracteres
Una referencia de carácter proporciona la unidad de código UTF16 de la instancia concreta [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] carácter se representa, en formato decimal o hexadecimal. El ejemplo siguiente muestra una referencia de carácter decimal para la letra mayúscula COPTO HORI o 'Ϩ':

```
&#1000;
```

El ejemplo siguiente muestra una referencia de carácter hexadecimal. Tenga en cuenta que tiene un **x** delante del número hexadecimal.

```
&#x3E8;
```

<a name="encoding"></a>
### <a name="encoding"></a>Codificación
 Las codificaciones compatibles con [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] son [!INCLUDE[TLA#tla_ascii](../../../../includes/tlasharptla-ascii-md.md)], [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] UTF-16 y UTF-8. La declaración de codificación está al principio de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] documento. Si no existe ningún atributo de codificación y no hay ningún orden de bytes, el analizador utiliza el valor predeterminado UTF-8. UTF-8 y UTF-16 son las codificaciones preferentes. No se admite UTF-7. En el ejemplo siguiente se muestra cómo especificar una codificación UTF-8 en un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] archivo.

```
?xml encoding="UTF-8"?
```

<a name="lang_attrib"></a>
### <a name="language-attribute"></a>Atributo de idioma
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] usa [XML: lang](../../xaml-services/xml-lang-handling-in-xaml.md) para representar el atributo de idioma de un elemento.  Para aprovechar la <xref:System.Globalization.CultureInfo> (clase), el valor del atributo de idioma debe ser uno de los nombres de referencias culturales predefinidos por <xref:System.Globalization.CultureInfo>. [xml:lang](../../xaml-services/xml-lang-handling-in-xaml.md) es heredable en el árbol de elementos (mediante reglas XML, no necesariamente debido a la herencia de las propiedades de dependencia) y su valor predeterminado es una cadena vacía si no se asigna de manera explícita.

 El atributo de idioma es muy útil para especificar dialectos. Por ejemplo, el francés tiene una ortografía, un vocabulario y una pronunciación diferentes en Francia, Quebec, Bélgica y Suiza. También el chino, japonés y coreano comparten puntos de código en [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)], pero las formas ideográficas son diferentes y utilizan fuentes totalmente distintas.

 La siguiente [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] en el ejemplo se usa el `fr-CA` atributo de idioma para especificar el francés canadiense.

```xml
<TextBlock xml:lang="fr-CA">Découvrir la France</TextBlock>
```

<a name="unicode"></a>
### <a name="unicode"></a>Unicode
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] todos los admite [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] características, incluidos los suplentes. Siempre y cuando el juego de caracteres que se puede asignar a [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)], que es compatible. Por ejemplo, GB18030 presenta algunos caracteres que se asignan a la extensión A y B de chino, japonés y coreano (CFK) y pares suplentes, por lo tanto, es totalmente compatible. Un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicación puede utilizar <xref:System.Globalization.StringInfo> para manipular las cadenas sin reconocer si tienen pares suplentes o caracteres combinables.

<a name="design_intl_ui_with_xaml"></a>
## <a name="designing-an-international-user-interface-with-xaml"></a>Diseñar una interfaz de usuario internacional con XAML
 Esta sección se describen [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] características que se deben considerar al escribir una aplicación.

<a name="intl_text"></a>
### <a name="international-text"></a>Texto internacional
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] incluye el procesamiento integrado para sistemas de escritura de todo Microsoft .NET Framework admitida.

 Actualmente se admiten los siguientes scripts:

-   Árabe

-   Bengalí

-   Devanagari

-   Cirílico

-   Griego

-   Gujarati

-   Gurmukhi

-   Hebreo

-   Scripts ideográficos

-   Canarés

-   Lao

-   Latín

-   Malayalam

-   Mongol

-   Odia

-   Siríaco

-   Tamul

-   Telugu

-   Thaana

-   Tailandés*

-   Tibetano

 * En esta versión, la visualización y edición de texto tailandés es compatible; no lo es la separación de palabras.

 Actualmente no se admiten los siguientes scripts:

-   Jemer

-   Hangul coreano antiguo

-   Birmano

-   Cingalés

 Compatibilidad con motores de todo el sistema de escritura [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] fuentes. [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] las fuentes pueden incluir el [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] tablas de diseño que permiten a los creadores de fuentes diseñar fuentes tipográficas mejor internacionales y avanzadas. El [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] tablas de diseño de fuente contienen información sobre las sustituciones, posicionamiento de glifo, justificación y posición de línea base, permitir que las aplicaciones de procesamiento de texto mejorar el diseño de texto.

 [!INCLUDE[TLA2#tla_opentype](../../../../includes/tla2sharptla-opentype-md.md)] las fuentes permiten el control de glifo de grande conjuntos mediante [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] codificación. Esta codificación permite una amplia compatibilidad internacional, así como variantes tipográficas de los glifos.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] representación de texto cuenta con la tecnología [!INCLUDE[TLA#tla_ct](../../../../includes/tlasharptla-ct-md.md)] tecnología de subpíxeles compatible con independencia de la resolución. Esto mejora significativamente la legibilidad y permite la capacidad de admitir documentos de estilo de revista de gran calidad para todos los scripts.

<a name="intl_layout"></a>
### <a name="international-layout"></a>Diseño internacional
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] proporciona una manera muy cómoda de admitir diseños horizontales, bidireccionales y verticales. En el marco de presentación del <xref:System.Windows.FrameworkElement.FlowDirection%2A> propiedad puede usarse para definir el diseño. Los patrones de dirección de flujo son:

-   *LeftToRight*: diseño horizontal para latín, Asia Oriental y demás.

-   *RightToLeft*: bidireccional para árabe, hebreo y demás.

<a name="developing_localizable_apps"></a>
## <a name="developing-localizable-applications"></a>Desarrollar aplicaciones localizables
 Al escribir una aplicación para su consumo global, debe tener en cuenta que la aplicación debe ser localizable. En los temas siguientes se señalan las cosas que deben tenerse en cuenta.

<a name="mui"></a>
### <a name="multilingual-user-interface"></a>Interfaz de usuario multilingüe
 Interfaces de usuario multilingüe (MUI) es un [!INCLUDE[TLA#tla_ms](../../../../includes/tlasharptla-ms-md.md)] soporte técnico para la modificación de [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] de un idioma a otro. Un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicación usa el modelo de conjunto para admitir la MUI. Una aplicación contiene los ensamblados neutrales respecto al idioma, así como los ensamblados de recursos satélite dependientes del idioma. El punto de entrada es un .EXE administrado en el ensamblado principal.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] cargador de recursos aprovecha la [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)]del Administrador de recursos para admitir la búsqueda de recursos y de respaldo. Varios ensamblados satélite de idioma funcionan con el mismo ensamblado principal. El ensamblado de recursos que se carga depende de la <xref:System.Globalization.CultureInfo.CurrentUICulture%2A> del subproceso actual.

<a name="localizable_ui"></a>
### <a name="localizable-user-interface"></a>Interfaz de usuario localizable
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] las aplicaciones utilizan [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] para definir sus [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] permite a los desarrolladores especificar una jerarquía de objetos con un conjunto de propiedades y lógica. El uso principal de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] es desarrollar [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicaciones pero puede utilizarse para especificar una jerarquía de cualesquiera [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] objetos. La mayoría de los desarrolladores usa [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] para especificar su aplicación [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] y usar un lenguaje de programación como C# para reaccionar a la interacción del usuario.

 Desde un punto de vista de recursos, un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] diseñado para describir un dependiente del idioma del archivo [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] es un elemento de recurso y, por tanto, su formato de distribución final debe ser localizable para admitir idiomas internacionales. Dado que [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] no se puede controlar eventos, muchas [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] aplicaciones contienen bloques de código para hacerlo. Para obtener más información, consulte [información general sobre XAML (WPF)](xaml-overview-wpf.md). Código se secciona y compila en archivos binarios diferentes cuando un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] archivo se convierte en el formulario BAML de XAML. Los archivos, imágenes y otros tipos de objetos de recursos administrados con formato BAML de XAML se insertan en el ensamblado de recursos satélite, que se puede localizar a otros idiomas, o en el ensamblado principal, cuando no se requiere la localización.

> [!NOTE]
>  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] las aplicaciones admiten todas las [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)] [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] recursos incluidos en las tablas de cadenas, imágenes y así sucesivamente.

<a name="building_localizable_apps"></a>
### <a name="building-localizable-applications"></a>Compilar aplicaciones localizables
 Localizar significa adaptar una [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] a distintas referencias culturales. Para realizar un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] sea localizable, los desarrolladores deben compilar todos los recursos localizables en un ensamblado de recursos de la aplicación. El ensamblado de recursos se localiza a distintos idiomas y el código subyacente utiliza la administración de recursos [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] para cargar. Uno de los archivos necesarios para un [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicación es un archivo de proyecto (.proj). Todos los recursos que se usan en la aplicación deben incluirse en el archivo de proyecto. En el ejemplo siguiente de un archivo .csproj se muestra cómo hacerlo.

```xml
<Resource Include="data\picture1.jpg"/>
<EmbeddedResource Include="data\stringtable.en-US.restext"/>
```

 Para usar un recurso de la aplicación, cree una instancia un <xref:System.Resources.ResourceManager> y cargue el recurso que desea usar. En el ejemplo siguiente se muestra cómo hacerlo:

 [!code-csharp[LocalizationResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]

<a name="using_clickonce"></a>
## <a name="using-clickonce-with-localized-applications"></a>Utilizar ClickOnce con aplicaciones localizadas
 ClickOnce es una nueva tecnología de implementación de Windows Forms que se suministrará con Visual Studio 2005. Permite la instalación y actualización de aplicaciones web. Cuando se localiza una aplicación que se implementó con ClickOnce, solo puede verse en la referencia cultural localizada. Por ejemplo, si una aplicación implementada se localiza a japonés solo puede verse en la versión japonesa [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] no en inglés de Windows. Esto presenta un problema porque es un escenario común para los usuarios japoneses ejecuten una versión en inglés de Windows.

 La solución a este problema es establecer el atributo neutro de reserva de idioma. Como alternativa, un desarrollador de aplicaciones puede quitar recursos del ensamblado principal y especificar que los recursos puedan encontrarse en un ensamblado satélite correspondiente a una referencia cultural específica. Para controlar este proceso, utilice el <xref:System.Resources.NeutralResourcesLanguageAttribute>. El constructor de la <xref:System.Resources.NeutralResourcesLanguageAttribute> clase tiene dos firmas, que toma un <xref:System.Resources.UltimateResourceFallbackLocation> parámetro para especificar la ubicación donde el <xref:System.Resources.ResourceManager> debe extraer la reserva de recursos: ensamblado principal o el ensamblado satélite. En el ejemplo siguiente se muestra cómo utilizar el atributo. Para la ubicación de reserva definitiva, el código hace que el <xref:System.Resources.ResourceManager> para buscar los recursos en el subdirectorio "de" del directorio del ensamblado actualmente en ejecución.

```
[assembly: NeutralResourcesLanguageAttribute(
    "de" , UltimateResourceFallbackLocation.Satellite)]
```

## <a name="see-also"></a>Vea también

- [Información general sobre la globalización y la localización de WPF](wpf-globalization-and-localization-overview.md)
