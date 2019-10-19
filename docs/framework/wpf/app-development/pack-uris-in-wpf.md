---
title: Empaquetar URI en WPF
ms.date: 03/30/2017
helpviewer_keywords:
- pack URI scheme [WPF]
- loading embedded resources [WPF]
- URIs (Uniform Resource Identifiers)
- Uniform Resource Identifiers (URIs)
- loading non-resource files
- application management [WPF]
ms.assetid: 43adb517-21a7-4df3-98e8-09e9cdf764c4
ms.openlocfilehash: 59c72d9ae12a014a8c47cb3b2852b337b173446c
ms.sourcegitcommit: 1f12db2d852d05bed8c53845f0b5a57a762979c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2019
ms.locfileid: "72580618"
---
# <a name="pack-uris-in-wpf"></a>Empaquetar URI en WPF

En Windows Presentation Foundation (WPF), los identificadores uniformes de recursos (URI) se usan para identificar y cargar archivos de muchas maneras, entre las que se incluyen las siguientes:

- Especificar el [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] que se va a mostrar cuando se inicia una aplicación por primera vez.

- Cargando imágenes.

- Navegando a páginas.

- Cargando archivos de datos no ejecutables.

Además, los URI se pueden usar para identificar y cargar archivos desde varias ubicaciones, incluidas las siguientes:

- Ensamblado actual.

- El ensamblado al que se hace referencia.

- Una ubicación relativa a un ensamblado.

- El sitio de origen de la aplicación.

Para proporcionar un mecanismo coherente para identificar y cargar estos tipos de archivos desde estas ubicaciones, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] aprovecha la extensibilidad del esquema de *pack uri*. En este tema se proporciona información general sobre el esquema, se explica cómo construir identificadores URI para una variedad de escenarios, se explican los URI absolutos y relativos y la resolución de identificadores URI, antes de mostrar cómo usar los URI del paquete de marcado y código.

<a name="The_Pack_URI_Scheme"></a>

## <a name="the-pack-uri-scheme"></a>Esquema de Pack URI

El esquema de Pack URI se usa en la especificación de [convenciones de empaquetado abierto](https://go.microsoft.com/fwlink/?LinkID=71255) (OPC), que describe un modelo para organizar e identificar el contenido. Los elementos clave de este modelo son paquetes y partes, donde un *paquete* es un contenedor lógico para una o más *partes*lógicas. La figura siguiente ilustra este concepto.

![Diagrama de paquete y partes](./media/pack-uris-in-wpf/wpf-package-parts-diagram.png)

Para identificar elementos, la especificación de OPC aprovecha la extensibilidad de RFC 2396 (identificadores uniformes de recursos (URI): Sintaxis genérica) para definir el esquema de Pack URI.

El esquema especificado por un URI se define mediante su prefijo; http, FTP y file son ejemplos conocidos. El esquema de Pack URI usa "Pack" como su esquema y contiene dos componentes: autoridad y ruta de acceso. A continuación se da el formato de un Pack URI.

*ruta* de / de la*autoridad* Pack://

La *autoridad* especifica el tipo de paquete que contiene una parte, mientras que la *ruta de acceso* especifica la ubicación de un elemento dentro de un paquete.

Este concepto se muestra en la ilustración siguiente:

![Relación entre paquete, autoridad y ruta de acceso](./media/pack-uris-in-wpf/wpf-relationship-diagram.png)

Los paquetes y los elementos son análogos a las aplicaciones y los archivos, donde una aplicación (paquete) puede incluir uno o más archivos (elementos), como los siguientes:

- Archivos de recursos que se compilan en el ensamblado local.

- Archivos de recursos que se compilan en un ensamblado al que se hace referencia.

- Archivos de recursos que se compilan en un ensamblado que hace referencia.

- Archivos de contenido.

- Archivos de sitio de origen.

Para tener acceso a estos tipos de archivos, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] admite dos entidades: application:///y siteoforigin:///. La autoridad application:/// identifica los archivos de datos de aplicación que se conocen en tiempo de compilación, incluidos los archivos de recursos y de contenido. La autoridad siteoforigin:/// identifica los archivos de sitio de origen. El ámbito de cada autoridad se muestra en la figura siguiente.

![Diagrama de URI de paquete](./media/pack-uris-in-wpf/wpf-pack-uri-scheme.png)

> [!NOTE]
> El componente de autoridad de un Pack URI es un identificador URI incrustado que apunta a un paquete y debe ajustarse a RFC 2396. Además, el carácter "/" se debe reemplazar por el carácter ",", y los caracteres reservados "%" y "?" deben incluirse en secuencias de escape. Consulte la especificación de OPC para detalles.

En las secciones siguientes se explica cómo construir Pack URI con estas dos autoridades junto con las rutas de acceso adecuadas para identificar los archivos de recursos, contenido y sitio de origen.

<a name="Resource_File_Pack_URIs___Local_Assembly"></a>

## <a name="resource-file-pack-uris"></a>Pack URI de archivos de recursos

Los archivos de recursos se configuran como elementos de `Resource` de MSBuild y se compilan en ensamblados. WPF admite la construcción de Pack URI que se pueden usar para identificar los archivos de recursos compilados en el ensamblado local o compilados en un ensamblado al que se hace referencia desde el ensamblado local.

<a name="Local_Assembly_Resource_File"></a>

### <a name="local-assembly-resource-file"></a>Archivo de recursos del ensamblado local

El Pack URI de un archivo de recursos que se compila en el ensamblado local usa la siguiente autoridad y ruta de acceso:

- **Autoridad**: application:///.

- **Ruta de acceso**: nombre del archivo de recursos, incluida su ruta de acceso relativa a la carpeta raíz del proyecto de ensamblado local.

En el ejemplo siguiente se muestra el Pack URI de un archivo de recursos de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que se encuentra en la raíz de la carpeta del proyecto del ensamblado local.

`pack://application:,,,/ResourceFile.xaml`

En el ejemplo siguiente se muestra el Pack URI de un archivo de recursos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que se encuentra en una subcarpeta de la carpeta del proyecto del ensamblado local.

`pack://application:,,,/Subfolder/ResourceFile.xaml`

<a name="Resource_File_Pack_URIs___Referenced_Assembly"></a>

### <a name="referenced-assembly-resource-file"></a>Archivo de recursos del ensamblado al que se hace referencia

El Pack URI de un archivo de recursos que se compila en un ensamblado al que se hace referencia usa la siguiente autoridad y ruta de acceso:

- **Autoridad**: application:///.

- **Ruta de acceso**: nombre de un archivo de recursos que se compila en un ensamblado al que se hace referencia. La ruta de acceso debe tener el formato siguiente:

  *AssemblyShortName*{ *; Versión*] { *; PublicKey*]; componente/*ruta de acceso*

  - **AssemblyShortName**: nombre corto del ensamblado al que se hace referencia.

  - **;Version** [opcional]: versión del ensamblado al que se hace referencia y que contiene el archivo de recursos. Se usa cuando hay cargados dos o más ensamblados a los que se hace referencia con el mismo nombre corto.

  - **;PublicKey** [opcional]: clave pública que se usó para firmar el ensamblado al que se hace referencia. Se usa cuando hay cargados dos o más ensamblados a los que se hace referencia con el mismo nombre corto.

  - **;component**: especifica que la referencia al ensamblado se hace desde el ensamblado local.

  - **/Path**: nombre del archivo de recursos, incluida su ruta de acceso relativa a la raíz de la carpeta del proyecto del ensamblado al que se hace referencia.

En el ejemplo siguiente se muestra el Pack URI de un archivo de recursos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que se encuentra en la raíz de la carpeta del proyecto del ensamblado al que se hace referencia.

`pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml`

En el ejemplo siguiente se muestra el Pack URI de un archivo de recursos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que se encuentra en una subcarpeta de la carpeta del proyecto del ensamblado al que se hace referencia.

`pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml`

En el ejemplo siguiente se muestra el Pack URI de un archivo de recursos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] que se encuentra en la carpeta raíz de una carpeta de proyecto de un ensamblado específico de la versión a la que se hace referencia.

`pack://application:,,,/ReferencedAssembly;v1.0.0.1;component/ResourceFile.xaml`

Tenga en cuenta que la sintaxis de Pack URI para los archivos de recursos de ensamblado a los que se hace referencia solo se puede usar con la autoridad application:///. Por ejemplo, no se admite lo siguiente en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].

`pack://siteoforigin:,,,/SomeAssembly;component/ResourceFile.xaml`

<a name="Content_File_Pack_URIs"></a>

## <a name="content-file-pack-uris"></a>Pack URI de archivos de contenido

El URI del paquete para un archivo de contenido usa la siguiente autoridad y ruta de acceso:

- **Autoridad**: application:///.

- **Ruta de acceso**: nombre del archivo de contenido, incluida su ruta de acceso relativa a la ubicación del sistema de archivos del ensamblado ejecutable principal de la aplicación.

En el ejemplo siguiente se muestra el Pack URI de un archivo de contenido de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], que se encuentra en la misma carpeta que el ensamblado ejecutable.

`pack://application:,,,/ContentFile.xaml`

En el ejemplo siguiente se muestra el Pack URI de un archivo de contenido de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)], que se encuentra en una subcarpeta relativa al ensamblado ejecutable de la aplicación.

`pack://application:,,,/Subfolder/ContentFile.xaml`

> [!NOTE]
> No se puede navegar por los archivos de contenido HTML. El esquema de URI solo admite la navegación a los archivos HTML que se encuentran en el sitio de origen.

<a name="The_siteoforigin_____Authority"></a>

## <a name="site-of-origin-pack-uris"></a>Pack URI de sitio de origen

El URI del paquete para un archivo de sitio de origen usa la siguiente autoridad y ruta de acceso:

- **Autoridad**: siteoforigin:///.

- **Ruta de acceso**: nombre del archivo de sitio de origen, incluida su ruta de acceso relativa a la ubicación desde donde se inició el ensamblado ejecutable.

En el ejemplo siguiente se muestra el Pack URI para un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] archivo de sitio de origen, almacenado en la ubicación desde la que se inicia el ensamblado ejecutable.

`pack://siteoforigin:,,,/SiteOfOriginFile.xaml`

En el ejemplo siguiente se muestra el Pack URI para un [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] archivo de sitio de origen, almacenado en una subcarpeta relativa a la ubicación desde la que se inicia el ensamblado ejecutable de la aplicación.

`pack://siteoforigin:,,,/Subfolder/SiteOfOriginFile.xaml`

<a name="Page_Files"></a>

## <a name="page-files"></a>Archivos de paginación

Los archivos XAML que se configuran como MSBuild `Page` elementos se compilan en ensamblados de la misma manera que los archivos de recursos. Por consiguiente, los elementos de `Page` de MSBuild se pueden identificar mediante pack uri para los archivos de recursos.

Los tipos de [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] archivos que se configuran normalmente como elementos `Page` de MSBuild tienen uno de los elementos siguientes como su elemento raíz:

- <xref:System.Windows.Window?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Page?displayProperty=nameWithType>

- <xref:System.Windows.Navigation.PageFunction%601?displayProperty=nameWithType>

- <xref:System.Windows.ResourceDictionary?displayProperty=nameWithType>

- <xref:System.Windows.Documents.FlowDocument?displayProperty=nameWithType>

- <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType>

<a name="Absolute_vs_Relative_Pack_URIs"></a>

## <a name="absolute-vs-relative-pack-uris"></a>URI absolutos frente a packs relativos

Un URI de paquete completo incluye el esquema, la autoridad y la ruta de acceso, y se considera un URI de paquete absoluto. Como simplificación de los desarrolladores, los elementos [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] normalmente permiten establecer los atributos adecuados con un URI de paquete relativo, que incluye solo la ruta de acceso.

Por ejemplo, considere el siguiente Pack URI absoluto para un archivo de recursos en el ensamblado local.

`pack://application:,,,/ResourceFile.xaml`

El URI del Pack relativo que hace referencia a este archivo de recursos sería el siguiente.

`/ResourceFile.xaml`

> [!NOTE]
> Dado que los archivos de sitio de origen no están asociados a los ensamblados, solo se puede hacer referencia a ellos con identificadores URI absolutos.

De forma predeterminada, un URI de Pack relativo se considera relativo a la ubicación del marcado o código que contiene la referencia. Sin embargo, si se usa una barra diagonal inversa inicial, la referencia del URI del Pack relativo se considera relativa a la raíz de la aplicación. Por ejemplo, considere la estructura de proyecto siguiente.

`App.xaml`

`Page2.xaml`

`\SubFolder`

`+ Page1.xaml`

`+ Page2.xaml`

Si página1. XAML contiene un URI que hace referencia a \SubFolder\Page2.XAML *raíz*, la referencia puede usar el siguiente URI de módulo relativo.

`Page2.xaml`

Si página1. XAML contiene un URI que hace referencia a \Page2.XAML *raíz*, la referencia puede usar el siguiente URI de módulo relativo.

`/Page2.xaml`

<a name="Pack_URI_Resolution"></a>

## <a name="pack-uri-resolution"></a>Resolución de Pack URI

El formato de los identificadores URI permite que los Pack URI de los distintos tipos de archivos tengan el mismo aspecto. Por ejemplo, considere el siguiente Pack URI absoluto.

`pack://application:,,,/ResourceOrContentFile.xaml`

Este URI de paquete absoluto podría hacer referencia a un archivo de recursos en el ensamblado local o en un archivo de contenido. Lo mismo se cumple para el URI relativo siguiente.

`/ResourceOrContentFile.xaml`

Con el fin de determinar el tipo de archivo al que hace referencia un Pack URI, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] resuelve los URI para los archivos de recursos en los ensamblados y archivos de contenido locales mediante el uso de la heurística siguiente:

1. Sondear los metadatos de ensamblado para un atributo de <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> que coincida con el URI del paquete.

2. Si se encuentra el atributo <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>, la ruta de acceso del Pack URI hace referencia a un archivo de contenido.

3. Si no se encuentra el atributo <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>, sondee los archivos de recursos de conjunto que se compilan en el ensamblado local.

4. Si se encuentra un archivo de recursos que coincide con la ruta de acceso del Pack URI, la ruta de acceso del Pack URI hace referencia a un archivo de recursos.

5. Si no se encuentra el recurso, el <xref:System.Uri> creado internamente no es válido.

La resolución de URI no se aplica a los URI que hacen referencia a lo siguiente:

- Archivos de contenido en ensamblados a los que se hace referencia: los [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] no admiten estos tipos de archivo.

- Archivos incrustados en ensamblados a los que se hace referencia: los URI que los identifican son únicos porque incluyen el nombre del ensamblado al que se hace referencia y el sufijo `;component`.

- Archivos de sitio de origen: los URI que los identifican son únicos porque son los únicos archivos que se pueden identificar mediante Pack URI que contienen la autoridad siteoforigin:///.

Una simplificación que la resolución de URI de paquete permite es que el código sea algo independiente de las ubicaciones de los archivos de recursos y de contenido. Por ejemplo, si tiene un archivo de recursos en el ensamblado local que se reconfigura para que sea un archivo de contenido, el URI del paquete del recurso sigue siendo el mismo, al igual que el código que usa el URI del paquete.

<a name="Programming_with_Pack_URIs"></a>

## <a name="programming-with-pack-uris"></a>Programación con Pack URI

Muchas clases de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] implementan propiedades que se pueden establecer con pack uri, entre los que se incluyen:

- <xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Frame.Source%2A?displayProperty=nameWithType>

- <xref:System.Windows.Navigation.NavigationWindow.Source%2A?displayProperty=nameWithType>

- <xref:System.Windows.Documents.Hyperlink.NavigateUri%2A?displayProperty=nameWithType>

- <xref:System.Windows.Window.Icon%2A?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Image.Source%2A?displayProperty=nameWithType>

Estas propiedades se pueden establecer tanto desde el marcado como desde el código. En esta sección se muestran las construcciones básicas para ambos y, luego, se muestran ejemplos de escenarios comunes.

<a name="Using_Pack_URIs_in_Markup"></a>

### <a name="using-pack-uris-in-markup"></a>Uso de los Pack URI en el marcado

Un Pack URI se especifica en el marcado estableciendo el elemento de un atributo con el Pack URI. Por ejemplo:

`<element attribute="pack://application:,,,/File.xaml" />`

En la tabla 1 se muestran los distintos identificadores URI absolutos que puede especificar en el marcado.

Tabla 1: Pack URI absolutos en el marcado

|Archivo|URI de paquete absoluto|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|Archivo de recursos: ensamblado local|`"pack://application:,,,/ResourceFile.xaml"`|
|Archivo de recursos en subcarpeta: ensamblado local|`"pack://application:,,,/Subfolder/ResourceFile.xaml"`|
|Archivo de recursos: ensamblado al que se hace referencia|`"pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml"`|
|Archivo de recursos en subcarpeta del ensamblado al que se hace referencia|`"pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml"`|
|Archivo de recursos en el ensamblado al que se hace referencia con versiones|`"pack://application:,,,/ReferencedAssembly;v1.0.0.0;component/ResourceFile.xaml"`|
|Archivo de contenido|`"pack://application:,,,/ContentFile.xaml"`|
|Archivo de contenido en subcarpeta|`"pack://application:,,,/Subfolder/ContentFile.xaml"`|
|Archivo de sitio de origen|`"pack://siteoforigin:,,,/SOOFile.xaml"`|
|Archivo de sitio de origen en subcarpeta|`"pack://siteoforigin:,,,/Subfolder/SOOFile.xaml"`|

En la tabla 2 se muestran los diversos identificadores URI relativos que se pueden especificar en el marcado.

Tabla 2: Pack URI relativos en el marcado

|Archivo|URI de paquete relativo|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|Archivo de recursos en el ensamblado local|`"/ResourceFile.xaml"`|
|Archivo de recursos en subcarpeta del ensamblado local|`"/Subfolder/ResourceFile.xaml"`|
|Archivo de recursos en el ensamblado al que se hace referencia|`"/ReferencedAssembly;component/ResourceFile.xaml"`|
|Archivo de recursos en subcarpeta del ensamblado al que se hace referencia|`"/ReferencedAssembly;component/Subfolder/ResourceFile.xaml"`|
|Archivo de contenido|`"/ContentFile.xaml"`|
|Archivo de contenido en subcarpeta|`"/Subfolder/ContentFile.xaml"`|

<a name="Using_Pack_URIs_in_Code"></a>

### <a name="using-pack-uris-in-code"></a>Uso de los Pack URI en el código

Para especificar un Pack URI en el código, cree una instancia de la clase <xref:System.Uri> y pase el URI del paquete como parámetro al constructor. Esto último se muestra en el ejemplo siguiente.

```csharp
Uri uri = new Uri("pack://application:,,,/File.xaml");
```

De forma predeterminada, la clase <xref:System.Uri> considera que los URI Pack son absolutos. Por consiguiente, se produce una excepción cuando se crea una instancia de la clase <xref:System.Uri> con un Pack URI relativo.

```csharp
Uri uri = new Uri("/File.xaml");
```

Afortunadamente, la sobrecarga <xref:System.Uri.%23ctor%28System.String%2CSystem.UriKind%29> del constructor de clase <xref:System.Uri> acepta un parámetro de tipo <xref:System.UriKind> para permitirle especificar si un Pack URI es absoluto o relativo.

```csharp
// Absolute URI (default)
Uri absoluteUri = new Uri("pack://application:,,,/File.xaml", UriKind.Absolute);
// Relative URI
Uri relativeUri = new Uri("/File.xaml",
                        UriKind.Relative);
```

Solo debe especificar <xref:System.UriKind.Absolute> o <xref:System.UriKind.Relative> cuando esté seguro de que el URI del paquete proporcionado es uno o el otro. Si no conoce el tipo de Pack URI que se usa, por ejemplo, cuando un usuario escribe un Pack URI en tiempo de ejecución, use <xref:System.UriKind.RelativeOrAbsolute> en su lugar.

```csharp
// Relative or Absolute URI provided by user via a text box
TextBox userProvidedUriTextBox = new TextBox();
Uri uri = new Uri(userProvidedUriTextBox.Text, UriKind.RelativeOrAbsolute);
```

En la tabla 3 se muestran los diversos Pack URI relativos que se pueden especificar en el código mediante <xref:System.Uri?displayProperty=nameWithType>.

Tabla 3: Pack URI absolutos en el código

|Archivo|URI de paquete absoluto|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|Archivo de recursos: ensamblado local|`Uri uri = new Uri("pack://application:,,,/ResourceFile.xaml", UriKind.Absolute);`|
|Archivo de recursos en subcarpeta: ensamblado local|`Uri uri = new Uri("pack://application:,,,/Subfolder/ResourceFile.xaml", UriKind.Absolute);`|
|Archivo de recursos: ensamblado al que se hace referencia|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml", UriKind.Absolute);`|
|Archivo de recursos en subcarpeta del ensamblado al que se hace referencia|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml", UriKind.Absolute);`|
|Archivo de recursos en el ensamblado al que se hace referencia con versiones|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;v1.0.0.0;component/ResourceFile.xaml", UriKind.Absolute);`|
|Archivo de contenido|`Uri uri = new Uri("pack://application:,,,/ContentFile.xaml", UriKind.Absolute);`|
|Archivo de contenido en subcarpeta|`Uri uri = new Uri("pack://application:,,,/Subfolder/ContentFile.xaml", UriKind.Absolute);`|
|Archivo de sitio de origen|`Uri uri = new Uri("pack://siteoforigin:,,,/SOOFile.xaml", UriKind.Absolute);`|
|Archivo de sitio de origen en subcarpeta|`Uri uri = new Uri("pack://siteoforigin:,,,/Subfolder/SOOFile.xaml", UriKind.Absolute);`|

En la tabla 4 se muestran los diversos Pack URI relativos que se pueden especificar en el código mediante <xref:System.Uri?displayProperty=nameWithType>.

Tabla 4: Pack URI relativos en el código

|Archivo|URI de paquete relativo|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|Archivo de recursos: ensamblado local|`Uri uri = new Uri("/ResourceFile.xaml", UriKind.Relative);`|
|Archivo de recursos en subcarpeta: ensamblado local|`Uri uri = new Uri("/Subfolder/ResourceFile.xaml", UriKind.Relative);`|
|Archivo de recursos: ensamblado al que se hace referencia|`Uri uri = new Uri("/ReferencedAssembly;component/ResourceFile.xaml", UriKind.Relative);`|
|Archivo de recursos en subcarpeta: ensamblado al que se hace referencia|`Uri uri = new Uri("/ReferencedAssembly;component/Subfolder/ResourceFile.xaml", UriKind.Relative);`|
|Archivo de contenido|`Uri uri = new Uri("/ContentFile.xaml", UriKind.Relative);`|
|Archivo de contenido en subcarpeta|`Uri uri = new Uri("/Subfolder/ContentFile.xaml", UriKind.Relative);`|

<a name="Common_Pack_URI_Scenarios"></a>

### <a name="common-pack-uri-scenarios"></a>Escenarios comunes de Pack URI

En las secciones anteriores se ha explicado cómo construir pack uri para identificar los archivos de recursos, contenido y sitio de origen. En [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], estas construcciones se utilizan de varias maneras, y las secciones siguientes cubren varios usos comunes.

<a name="Specifying_the_UI_to_Show_when_an_Application_Starts"></a>

#### <a name="specifying-the-ui-to-show-when-an-application-starts"></a>Especificación de la UI que se va a mostrar cuando una aplicación se inicia por primera vez

<xref:System.Windows.Application.StartupUri%2A> especifica el primer [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] que se va a mostrar cuando se inicia una aplicación [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]. En el caso de las aplicaciones independientes, el [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] puede ser una ventana, tal como se muestra en el ejemplo siguiente.

[!code-xaml[PackURIOverviewSnippets#StartupUriWindow](~/samples/snippets/csharp/VS_Snippets_Wpf/PackURIOverviewSnippets/CS/Copy of App.xaml#startupuriwindow)]

Las aplicaciones y [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] independientes también pueden especificar una página como la interfaz de usuario inicial, como se muestra en el ejemplo siguiente.

[!code-xaml[PackURIOverviewSnippets#StartupUriPage](~/samples/snippets/csharp/VS_Snippets_Wpf/PackURIOverviewSnippets/CS/App.xaml#startupuripage)]

Si la aplicación es una aplicación independiente y se especifica una página con <xref:System.Windows.Application.StartupUri%2A>, [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] abre un <xref:System.Windows.Navigation.NavigationWindow> para hospedar la página. Por [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)], la página se muestra en el explorador del host.

<a name="Navigating_to_a_Page"></a>

#### <a name="navigating-to-a-page"></a>Navegación a una página

En el ejemplo siguiente se muestra cómo navegar a una página.

[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml1)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml2)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml3)]

Para obtener más información sobre las distintas maneras de navegar en [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], consulte [información general sobre navegación](navigation-overview.md).

<a name="Specifying_a_Window_Icon"></a>

#### <a name="specifying-a-window-icon"></a>Especificación de un icono de ventana

En el ejemplo siguiente se muestra cómo usar un identificador URI para especificar el icono de una ventana.

[!code-xaml[WindowIconSnippets#WindowIconSetXAML](~/samples/snippets/xaml/VS_Snippets_Wpf/WindowIconSnippets/XAML/MainWindow.xaml#windowiconsetxaml)]

Para obtener más información, vea <xref:System.Windows.Window.Icon%2A>.

<a name="Loading_Image__Audio__and_Video_Files"></a>

#### <a name="loading-image-audio-and-video-files"></a>Carga de archivos de imagen, audio y vídeo

[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] permite a las aplicaciones usar una amplia variedad de tipos de medios, todos ellos se pueden identificar y cargar con pack uri, como se muestra en los ejemplos siguientes.

[!code-xaml[MediaPlayerVideoSample#VideoPackURIAtSOO](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaPlayerVideoSample/CS/HomePage.xaml#videopackuriatsoo)]

[!code-xaml[MediaPlayerAudioSample#AudioPackURIAtSOO](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaPlayerAudioSample/CS/HomePage.xaml#audiopackuriatsoo)]

[!code-xaml[ImageSample#ImagePackURIContent](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageSample/CS/HomePage.xaml#imagepackuricontent)]

Para obtener más información sobre cómo trabajar con contenido multimedia, vea [gráficos y multimedia](../graphics-multimedia/index.md).

<a name="Loading_a_Resource_Dictionary_from_the_Site_of_Origin"></a>

#### <a name="loading-a-resource-dictionary-from-the-site-of-origin"></a>Carga de un diccionario de recursos desde el sitio de origen

Los diccionarios de recursos (<xref:System.Windows.ResourceDictionary>) se pueden usar para admitir los temas de la aplicación. Una forma de crear y administrar temas consiste en crear varios temas como diccionarios de recursos que están ubicados en el sitio de origen de una aplicación. Esto permite agregar temas y actualizarlos sin tener que volver a compilar e implementar una aplicación. Estos diccionarios de recursos se pueden identificar y cargar mediante pack uri, que se muestra en el ejemplo siguiente.

[!code-xaml[ResourceDictionarySnippets#ResourceDictionaryPackURI](~/samples/snippets/csharp/VS_Snippets_Wpf/ResourceDictionarySnippets/CS/App.xaml#resourcedictionarypackuri)]

Para obtener información general sobre los temas de [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], consulte [aplicar estilos y plantillas](../controls/styling-and-templating.md).

## <a name="see-also"></a>Vea también

- [Archivos de recursos, contenido y datos de aplicaciones de WPF](wpf-application-resource-content-and-data-files.md)
