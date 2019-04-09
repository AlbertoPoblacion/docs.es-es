---
title: Empaquetar fuentes con aplicaciones
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applications [WPF], packaging fonts with
- fonts [WPF], packaging with applications
- typography [WPF], packaging fonts with applications
- packaging fonts with applications [WPF]
ms.assetid: db15ee48-4d24-49f5-8b9d-a64460865286
ms.openlocfilehash: fb91d4b413db512021b90f0d4ba3049fe7333601
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59123804"
---
# <a name="packaging-fonts-with-applications"></a>Empaquetar fuentes con aplicaciones
Este tema proporciona información general sobre cómo empaquetar fuentes con su [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] aplicación.  
  
> [!NOTE]
>  Como con la mayoría de los tipos de software, los archivos de fuentes se otorgan bajo licencia, no se venden. Licencias que rigen el uso de las fuentes varían según el proveedor, pero en general mayoría de las licencias, incluidos aquellos que abarcan las fuentes [!INCLUDE[TLA#tla_ms#initcap](../../../../includes/tlasharptla-mssharpinitcap-md.md)] con aplicaciones y [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)], no se permiten las fuentes incrustadas dentro de las aplicaciones o en caso contrario redistribuir. Así pues, como programador, su responsabilidad es asegurarse de disponer de los derechos de licencia necesarios para cualquier fuente que incruste en una aplicación o redistribuya de cualquier otro modo.  

<a name="introduction_to_packaging_fonts"></a>   
## <a name="introduction-to-packaging-fonts"></a>Introducción al empaquetado de fuentes  
 Puede empaquetar fuentes fácilmente como recursos dentro de su [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] contenido basado en aplicaciones para mostrar texto de la interfaz de usuario y otros tipos de texto. Las fuentes pueden ser independientes de los archivos de ensamblado de la aplicación o incrustadas en dichos archivos. También puede crear una biblioteca de fuentes solo de recursos, a la que puede hacer referencia la aplicación.  
  
 [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] y [!INCLUDE[TLA#tla_truetype](../../../../includes/tlasharptla-truetype-md.md)] fuentes contienen un indicador de tipo, fsType, que indica los derechos de licencia de incrustación de fuente para la fuente. Sin embargo, este tipo de marca solo hace referencia a fuentes incrustadas almacenadas en un documento: no hace referencia a fuentes incrustadas en una aplicación. Puede recuperar la fuente de incrustación de derechos para una fuente mediante la creación de un <xref:System.Windows.Media.GlyphTypeface> objeto y hacer referencia a su <xref:System.Windows.Media.GlyphTypeface.EmbeddingRights%2A> propiedad. Consulte la sección "OS/2 y métricas de Windows" de la [especificación OpenType](https://www.microsoft.com/typography/otspec/os2.htm) para obtener más información sobre la marca fsType.  
  
 El [Microsoft Typography](https://docs.microsoft.com/typography/) sitio Web incluye información de contacto que puede ayudarle a encontrar un proveedor de fuentes determinado o un proveedor de fuentes para trabajos personalizados.  
  
<a name="adding_fonts_as_content_items"></a>   
## <a name="adding-fonts-as-content-items"></a>Agregar fuentes como elementos de contenido  
 Puede agregar las fuentes a la aplicación como elementos de contenido del proyecto independientes de los archivos de ensamblado de la aplicación. Esto significa que los elementos de contenido no se incrustan como recursos en un ensamblado. En el siguiente ejemplo de archivo de proyecto se muestra cómo definir elementos de contenido.  
  
```xml  
<Project DefaultTargets="Build"  
                xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Content Include="Peric.ttf" />  
    <Content Include="Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
 Para asegurarse de que la aplicación puede usar las fuentes en tiempo de ejecución, las fuentes deben ser accesibles en el directorio de implementación de la aplicación. El `<CopyToOutputDirectory>` elemento en el archivo de proyecto de la aplicación permite copiar automáticamente las fuentes en el directorio de implementación de aplicación durante el proceso de compilación. En el siguiente ejemplo de archivo de proyecto se muestra cómo copiar las fuentes en el directorio de implementación.  
  
```xml  
<ItemGroup>  
  <Content Include="Peric.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
  <Content Include="Pericl.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
</ItemGroup>  
```  
  
 En el ejemplo de código siguiente se muestra cómo hacer referencia a la fuente de la aplicación como un elemento de contenido: el elemento de contenido al que se hace referencia debe estar en el mismo directorio que los archivos de ensamblado de la aplicación.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet8](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet8)]  
  
<a name="adding_fonts_as_resource_items"></a>   
## <a name="adding-fonts-as-resource-items"></a>Agregar fuentes como elementos de recursos  
 Puede agregar fuentes a la aplicación como elementos de recursos del proyecto incrustados dentro de los archivos de ensamblado de la aplicación. Usar un subdirectorio independiente para los recursos ayuda a organizar los archivos de proyecto de la aplicación. En el siguiente ejemplo de archivo de proyecto se muestra cómo definir las fuentes como elementos de recursos en un subdirectorio independiente.  
  
```xml  
<Project DefaultTargets="Build"  
                xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Resource Include="resources\Peric.ttf" />  
    <Resource Include="resources\Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
> [!NOTE]
>  Al agregar fuentes como recursos de su aplicación, asegúrese de que está configurando el `<Resource>` elemento y no el `<EmbeddedResource>` elemento en el archivo de proyecto de la aplicación. El `<EmbeddedResource>` (elemento) para la acción de compilación no se admite.  
  
 En el ejemplo de marcado siguiente se muestra cómo hacer referencia a los recursos de fuentes de la aplicación.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet1)]  
  
### <a name="referencing-font-resource-items-from-code"></a>Hacer referencia a elementos de recursos de fuentes desde el código  
 Para hacer referencia a elementos de recursos de fuentes desde el código, debe proporcionar una referencia de recurso de fuentes de dos partes: la base de [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]; y la referencia de ubicación de la fuente. Estos valores se usan como parámetros para el <xref:System.Windows.Media.FontFamily.%23ctor%2A> método. El ejemplo de código siguiente muestra cómo hacer referencia a los recursos de fuentes de la aplicación en el subdirectorio de proyecto llamado `resources`.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet2)]
 [!code-vb[FontSnippets#FontPackageSnippet2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet2)]  
  
 La base de [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] puede incluir el subdirectorio de aplicación donde reside el recurso de fuente. En este caso, la referencia de ubicación de la fuente no necesitará especificar un directorio, pero tendría que incluir los caracteres iniciales "`./`", lo que indica que el recurso de fuente está en el mismo directorio especificado por la base de [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]. En el ejemplo de código siguiente se muestra una manera alternativa de hacer referencia al elemento de recursos de fuentes: es equivalente al ejemplo de código anterior.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet5)]
 [!code-vb[FontSnippets#FontPackageSnippet5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet5)]  
  
### <a name="referencing-fonts-from-the-same-application-subdirectory"></a>Hacer referencia a fuentes desde el mismo subdirectorio de aplicación  
 Puede colocar archivos de contenido y de recursos de aplicación dentro del mismo subdirectorio definido por el usuario del proyecto de la aplicación. En el siguiente ejemplo de archivo de proyecto se muestra una página de contenido y recursos de fuentes definidos en el mismo subdirectorio.  
  
```xml  
<ItemGroup>  
  <Page Include="pages\HomePage.xaml" />  
</ItemGroup>  
<ItemGroup>  
  <Resource Include="pages\Peric.ttf" />  
  <Resource Include="pages\Pericl.ttf" />  
</ItemGroup>  
```  
  
 Puesto que el contenido de la aplicación y la fuente están en el mismo subdirectorio, la referencia de fuentes está relacionada con el contenido de la aplicación. En los ejemplos siguientes se muestra cómo hacer referencia a recursos de fuentes de la aplicación cuando la fuente está en el mismo directorio que la aplicación.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml#fontpackagesnippet3)]  
  
 [!code-csharp[FontSnippets#FontPackageSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml.cs#fontpackagesnippet4)]
 [!code-vb[FontSnippets#FontPackageSnippet4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/pages/homepage.xaml.vb#fontpackagesnippet4)]  
  
### <a name="enumerating-fonts-in-an-application"></a>Enumerar fuentes en una aplicación  
 Para enumerar las fuentes como elementos de recursos en la aplicación, use la <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> o <xref:System.Windows.Media.Fonts.GetTypefaces%2A> método. El ejemplo siguiente muestra cómo usar el <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> método para devolver la colección de <xref:System.Windows.Media.FontFamily> objetos desde la ubicación de fuentes de la aplicación. En este caso, la aplicación contiene un subdirectorio llamado "resources".  
  
 [!code-csharp[FontSnippets#FontsSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet3)]
 [!code-vb[FontSnippets#FontsSnippet3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet3)]  
  
 El ejemplo siguiente muestra cómo usar el <xref:System.Windows.Media.Fonts.GetTypefaces%2A> método para devolver la colección de <xref:System.Windows.Media.Typeface> objetos desde la ubicación de fuentes de la aplicación. En este caso, la aplicación contiene un subdirectorio llamado "resources".  
  
 [!code-csharp[FontSnippets#FontsSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet7)]
 [!code-vb[FontSnippets#FontsSnippet7](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet7)]  
  
<a name="creating_a_font_resource_library"></a>   
## <a name="creating-a-font-resource-library"></a>Crear una biblioteca de recursos de fuentes  
 Puede crear una biblioteca solo de recursos que contenga solo fuentes: ningún código forma parte de este tipo de proyecto de biblioteca. Crear una biblioteca solo de recursos es una técnica común para desacoplar los recursos del código de aplicación que los usa. Esto también permite que el ensamblado de biblioteca se incluya con varios proyectos de aplicación. En el siguiente ejemplo de archivo de proyecto se muestran las partes clave de un proyecto de biblioteca solo de recursos.  
  
```xml  
<PropertyGroup>  
  <AssemblyName>FontLibrary</AssemblyName>  
  <OutputType>library</OutputType>  
  ...  
</PropertyGroup>  
...  
<ItemGroup>  
  <Resource Include="Kooten.ttf" />  
  <Resource Include="Pesca.ttf" />  
</ItemGroup  
```  
  
### <a name="referencing-a-font-in-a-resource-library"></a>Hacer referencia a una fuente en una biblioteca de recursos  
 Para hacer referencia a una fuente en una biblioteca de recursos de la aplicación, debe anteponer la referencia de la fuente con el nombre del ensamblado de la biblioteca. En este caso, el ensamblado de recursos de fuentes es "FontLibrary". Para separar el nombre del ensamblado de la referencia dentro del ensamblado, use un carácter ";". Agregar la palabra clave "Component" seguida de la referencia al nombre de la fuente completa toda la referencia en el recurso de la biblioteca de fuentes. En el ejemplo de código siguiente se muestra cómo hacer referencia a una fuente en un ensamblado de biblioteca de recursos.  
  
 [!code-xaml[OpenTypeFontsSample#OpenTypeFontsSample1](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontsSample/CS/Kootenay.xaml#opentypefontssample1)]  
  
> [!NOTE]
>  Este SDK contiene un conjunto de ejemplo [!INCLUDE[TLA#tla_opentype](../../../../includes/tlasharptla-opentype-md.md)] fuentes que puede usar con [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicaciones. Las fuentes se definen en una biblioteca solo de recursos. Para obtener más información, vea [Paquete de fuentes OpenType de ejemplo](sample-opentype-font-pack.md).  
  
<a name="limitations_on_font_usage"></a>   
## <a name="limitations-on-font-usage"></a>Limitaciones de uso de fuentes  
 En la lista siguiente se describe varias limitaciones sobre el empaquetado y el uso de fuentes en [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicaciones:  
  
-   **Bits de permisos de incrustación de fuentes:** las aplicaciones [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] no comprueban ni exigen ningún bit de permisos de incrustación de fuentes. Consulte la [Introducción al empaquetado fuentes](#introduction_to_packaging_fonts) sección para obtener más información.  
  
-   **Sitio de fuentes de origen:** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicaciones no permiten una referencia de fuente para http o ftp [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)].  
  
-   **URI absoluto con el paquete: notación:** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] aplicaciones no permiten crear un <xref:System.Windows.Media.FontFamily> mediante programación a través de objetos "pack:" como parte de absolutos [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] referencia a una fuente. Por ejemplo, `"pack://application:,,,/resources/#Pericles Light"` es una referencia de fuente no válida.  
  
-   **Incrustación de fuentes automática:** Durante el tiempo de diseño, no hay ninguna compatibilidad para la búsqueda de uso de la aplicación de las fuentes e incrustar fuentes automáticamente en recursos de la aplicación.  
  
-   **Subconjuntos de fuentes:** las aplicaciones [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] no admiten la creación de subconjuntos de fuentes para documentos no fijos.  
  
-   En casos donde hay una referencia incorrecta, la aplicación vuelve a usar una fuente disponible.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Documents.Typography>
- <xref:System.Windows.Media.FontFamily>
- [Microsoft Typography: Vínculos, noticias y contactos](https://docs.microsoft.com/typography/)
- [Especificación OpenType](https://www.microsoft.com/typography/otspec/)
- [Características de las fuentes OpenType](opentype-font-features.md)
- [Paquete de fuentes OpenType de ejemplo](sample-opentype-font-pack.md)
