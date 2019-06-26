---
title: Recursos de aplicación para bibliotecas destinadas a varias plataformas
ms.date: 07/18/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- multiple platforms, resources for
- resources [.NET Framework]
- .NET Framework, resources when targeting multiple platforms
- resources, for multiple platforms
- targeting multiple platforms, resources for
ms.assetid: 72c76f0b-7255-4576-9261-3587f949669c
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ba4546397adcfcf6142b41482f574cf86607a6b9
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2019
ms.locfileid: "67402114"
---
# <a name="app-resources-for-libraries-that-target-multiple-platforms"></a>Recursos de aplicación para bibliotecas destinadas a varias plataformas
Puede usar .NET Framework [biblioteca de clases Portable](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) tipo para asegurarse de que se pueden tener acceso a recursos en las bibliotecas de clases desde varias plataformas de proyecto. Este tipo de proyecto está disponible en Visual Studio 2012 y tiene como destino el subconjunto portable de la biblioteca de clases de .NET Framework. Mediante la [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] se garantiza que se pueda obtener acceso a la biblioteca desde las aplicaciones de escritorio, aplicaciones Silverlight, aplicaciones Windows Phone y aplicaciones de la [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

 El proyecto de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] es solo un subconjunto muy limitado de los tipos del espacio de nombres <xref:System.Resources> disponible para la aplicación, pero podrá usar la clase <xref:System.Resources.ResourceManager> para recuperar recursos. Sin embargo, si está creando una aplicación mediante el uso de Visual Studio, debe usar el contenedor fuertemente tipado creado con Visual Studio en lugar de utilizar la clase <xref:System.Resources.ResourceManager> directamente.

 Para crear un contenedor fuertemente tipado en Visual Studio, establezca el archivo de recursos principal **modificador de acceso** en el Diseñador de recursos de Visual Studio para **pública**. Esto crea un archivo [nombreArchivoRecursos].designer.cs o [nombreArchivoRecursos].designer.vb que incluye el contenedor ResourceManager fuertemente tipado. Para obtener más información sobre el uso de un contenedor de recursos fuertemente tipados, vea la sección "Generar una clase fuertemente tipados recursos" en el [Resgen.exe (Resource File Generator)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) tema.

## <a name="resource-manager-in-the-includenetportableincludesnet-portable-mdmd"></a>Administrador de recursos en la [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]
 En un proyecto de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], todo el acceso a los recursos lo controla la clase <xref:System.Resources.ResourceManager>. Dado que no se puede tener acceso a los tipos del espacio de nombres <xref:System.Resources>, como <xref:System.Resources.ResourceReader> y <xref:System.Resources.ResourceSet>, desde un proyecto de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], estos no pueden utilizarse para obtener acceso a los recursos.

 El proyecto de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] incluye los cuatro miembros de <xref:System.Resources.ResourceManager> que se enumeran en la tabla siguiente. Estos constructores y métodos permiten crear una instancia de un objeto <xref:System.Resources.ResourceManager> y recuperar recursos de cadena.

|Miembro`ResourceManager`|Descripción|
|------------------------------|-----------------|
|<xref:System.Resources.ResourceManager.%23ctor%28System.String%2CSystem.Reflection.Assembly%29>|Crea una instancia de <xref:System.Resources.ResourceManager> para obtener acceso al archivo de recursos con nombre que se encuentra en el ensamblado especificado.|
|<xref:System.Resources.ResourceManager.%23ctor%28System.Type%29>|Crea una instancia de <xref:System.Resources.ResourceManager> que corresponde al tipo especificado.|
|<xref:System.Resources.ResourceManager.GetString%28System.String%29>|Recupera un recurso con nombre para la referencia cultural actual.|
|<xref:System.Resources.ResourceManager.GetString%28System.String%2CSystem.Globalization.CultureInfo%29>|Recupera un recurso con nombre que pertenece a la referencia cultural especificada.|

 La exclusión de otros miembros de <xref:System.Resources.ResourceManager> de la [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] significa que no pueden recuperarse objetos serializados, datos que no son de cadena e imágenes de un archivo de recursos. Para usar los recursos de una [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], debe almacenar todos los datos de objeto en formato de cadena. Por ejemplo, para almacenar valores numéricos en un archivo de recursos, estos pueden convertirse en cadenas. A continuación, podrán recuperarse y convertirse de nuevo en números con los métodos `Parse` o `TryParse` del tipo de datos numérico. Puede convertir imágenes u otros datos binarios en una representación de cadena mediante una llamada al método <xref:System.Convert.ToBase64String%2A?displayProperty=nameWithType> y restaurarlos en una matriz de bytes mediante una llamada al método <xref:System.Convert.FromBase64String%2A?displayProperty=nameWithType>.

## <a name="the-includenetportableincludesnet-portable-mdmd-and-windows-store-apps"></a>Aplicaciones de la [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] y la Tienda Windows
 Los proyectos de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] almacenan recursos en archivos .resx que, a continuación, se compilan en archivos .resources y se incrustan en el ensamblado principal o en los ensamblados satélite en tiempo de compilación. Por otro lado, las aplicaciones de la [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] requieren que los recursos se almacenen en archivos .resw, que se compilan en un archivo de índice de recursos del paquete (PRI) único. Sin embargo, a pesar de los formatos de archivo incompatibles, la [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] funcionará en una aplicación de la [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)].

 Para usar la biblioteca de clases desde una aplicación de la [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], agregue una referencia a esta en el proyecto de aplicación de la Tienda Windows. Visual Studio extraerá los recursos del ensamblado en un archivo .resw y usarlo para generar un archivo PRI desde el que el tiempo de ejecución de Windows puede extraer los recursos de forma transparente. En tiempo de ejecución, el tiempo de ejecución de Windows se ejecuta el código en su [!INCLUDE[net_portable](../../../includes/net-portable-md.md)], pero recupera los recursos de la biblioteca de clases Portable desde el archivo PRI.

 Si el proyecto de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] incluye recursos localizados, se usa el modelo de concentrador y radio para implementarlos como se haría con una biblioteca en una aplicación de escritorio. Para consumir el archivo de recursos principal y cualquier archivo de recursos localizado en la aplicación de la [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], se agrega una referencia al ensamblado principal. En tiempo de compilación, Visual Studio extrae los recursos del archivo de recursos principal y de cualquier archivo de recursos localizado en archivos .resw independientes. A continuación, se compila los archivos .resw en un único archivo PRI que tiene acceso el tiempo de ejecución de Windows en tiempo de ejecución.

<a name="NonLoc"></a>
## <a name="example-non-localized-includenetportableincludesnet-portable-mdmd"></a>Ejemplo: No localizado [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]
 En el siguiente ejemplo sencillo de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] no localizada, se usan recursos para almacenar los nombres de columnas y para determinar el número de caracteres que se van a reservar para los datos tabulares. En el ejemplo se usa un archivo denominado LibResources.resx para almacenar los recursos de cadena que se enumeran en la tabla siguiente.

|Nombre del recurso|Valor del recurso|
|-------------------|--------------------|
|Born|Fecha de nacimiento|
|BornLength|12|
|Hired|Fecha de contratación|
|HiredLength|12|
|ID|ID|
|ID.Length|12|
|Name|Name|
|NameLength|25|
|Título|Base de datos de empleados|

 El código siguiente define un `UILibrary` clase que usa el contenedor del Administrador de recursos denominado `resources` generado por Visual Studio cuando el **modificador de acceso** para el archivo se cambia a **pública** . La clase UILibrary analiza los datos de cadena según sea necesario. . Tenga en cuenta que la clase está en el espacio de nombres `MyCompany.Employees`.

 [!code-csharp[Conceptual.Resources.Portable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/uilibrary.cs#1)]
 [!code-vb[Conceptual.Resources.Portable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/uilibrary.vb#1)]

 El código siguiente muestra cómo obtener acceso a la clase `UILibrary` y a sus recursos desde una aplicación de modo de consola. Requiere una referencia a UILibrary.dll al agregarse al proyecto de aplicación de consola.

 [!code-csharp[Conceptual.Resources.Portable#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program.cs#2)]
 [!code-vb[Conceptual.Resources.Portable#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module1.vb#2)]

 El código siguiente muestra cómo obtener acceso a la clase `UILibrary` y a sus recursos desde una aplicación de la [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Requiere una referencia a UILibrary.dll al agregarse al proyecto de aplicación de Windows Store.

 [!code-csharp[Conceptual.Resources.PortableMetro#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetro/cs/blankpage.xaml.cs#1)]

## <a name="example-localized-includenetportableincludesnet-portable-mdmd"></a>Ejemplo: Localizado [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]
 El siguiente ejemplo de [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] localizada incluye recursos para las referencias culturales de francés (Francia) e inglés (Estados Unidos). La referencia cultural inglés (Estados Unidos) es la referencia cultural predeterminada de la aplicación; sus recursos se muestran en la tabla en la [sección anterior](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md#NonLoc). El archivo de recursos de la referencia cultural Francés (Francia) se denomina LibResources.fr-FR.resx y consta de los recursos de cadena que se enumeran en la tabla siguiente. El código fuente para la clase `UILibrary` es el mismo que se muestra en la sección anterior.

|Nombre del recurso|Valor del recurso|
|-------------------|--------------------|
|Born|Date de naissance|
|BornLength|20|
|Hired|Date embauché|
|HiredLength|16|
|ID|ID|
|Name|Nom|
|Título|Base de données des employés|

 El código siguiente muestra cómo obtener acceso a la clase `UILibrary` y a sus recursos desde una aplicación de modo de consola. Requiere una referencia a UILibrary.dll al agregarse al proyecto de aplicación de consola.

 [!code-csharp[Conceptual.Resources.Portable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program2.cs#3)]
 [!code-vb[Conceptual.Resources.Portable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module2.vb#3)]

 El código siguiente muestra cómo obtener acceso a la clase `UILibrary` y a sus recursos desde una aplicación de la [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Requiere una referencia a UILibrary.dll al agregarse al proyecto de aplicación de Windows Store. Usa la propiedad estática `ApplicationLanguages.PrimaryLanguageOverride` para establecer el idioma preferido de la aplicación en francés.

 [!code-csharp[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetroloc/cs/blankpage.xaml.cs#1)]
 [!code-vb[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portablemetroloc/vb/blankpage.xaml.vb#1)]  
  
## <a name="see-also"></a>Vea también

- <xref:System.Resources.ResourceManager>
- [Recursos de aplicaciones de escritorio](../../../docs/framework/resources/index.md)
- [Empaquetar e implementar recursos](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)
