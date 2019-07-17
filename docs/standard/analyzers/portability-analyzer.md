---
title: Analizador de portabilidad de .NET | .NET
description: Obtenga información sobre cómo usar la herramienta Analizador de portabilidad de .NET para evaluar la portabilidad de su código entre las diferentes implementaciones de .NET, incluidos .NET Core, .NET Standard, UWP y Xamarin.
ms.date: 07/10/2019
ms.technology: dotnet-standard
ms.assetid: 0375250f-5704-4993-a6d5-e21c499cea1e
ms.openlocfilehash: f05d4f4a2fce8fa9a4d2e334f44190ea37335038
ms.sourcegitcommit: 83ecdf731dc1920bca31f017b1556c917aafd7a0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2019
ms.locfileid: "67859782"
---
# <a name="the-net-portability-analyzer"></a>Analizador de portabilidad de .NET

¿Quiere que sus bibliotecas sean multiplataforma? ¿Desea saber cuánto trabajo se necesita para que la aplicación sea compatible con otras implementaciones y perfiles de .NET, incluidos .NET Core, .NET Standard, UWP y Xamarin para iOS, Android y Mac? El [Analizador de portabilidad de .NET](https://github.com/microsoft/dotnet-apiport) es una herramienta que le proporciona un informe detallado sobre el grado de flexibilidad de su programa en las implementaciones de .NET mediante el análisis de ensamblados. El analizador de portabilidad se ofrece como una [extensión de Visual Studio](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer), que analiza el ensamblado por proyecto y, como una [aplicación de consola ApiPort](https://aka.ms/apiportdownload), que analiza los ensamblados por archivos especificados o directorio.

## <a name="common-targets"></a>Destinos comunes

* [.NET Core](../../core/index.md): tiene un diseño modular, emplea el modo en paralelo y tiene como destino escenarios multiplataforma. El modo en paralelo permite adoptar nuevas versiones de .NET Core sin que ello afecte a otras aplicaciones. Si su objetivo es portar su aplicación a .NET Core compatible con varias plataformas, éste es el destino recomendado. 
* .[NET Standard](../../standard/net-standard.md): Incluye las API de .NET Standard disponibles en todas las implementaciones de .NET. Si su objetivo es que la biblioteca se ejecute en todas las plataformas compatibles con .NET, éste es el destino recomendado.  
* [ASP.NET Core](/aspnet/core): Un marco web moderno basado en .NET Core. Si su objetivo es portar su aplicación web a .NET Core para que sea compatible con varias plataformas, éste es el destino recomendado.
* .NET Core + [extensiones de plataforma](../../core/porting/windows-compat-pack.md): Incluye las API de .NET Core además del paquete de compatibilidad de Windows, que proporciona muchas de las tecnologías disponibles de .NET Framework. Se trata de un destino recomendado para la portabilidad de la aplicación de .NET Framework a .NET Core en Windows.
* .NET standard + [extensiones de la plataforma](../../core/porting/windows-compat-pack.md): Incluye las API de .NET Standard además del paquete de compatibilidad de Windows, que proporciona muchas de las tecnologías disponibles de .NET Framework. Se trata de un destino recomendado para la portabilidad de la biblioteca de .NET Framework a .NET Core en Windows.

## <a name="how-to-use-the-net-portability-analyzer"></a>Cómo usar el Analizador de portabilidad de .NET

Para empezar a usar el Analizador de portabilidad de .NET en Visual Studio, primero debe descargar e instalar la extensión desde [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Funciona en Visual Studio 2017 y versiones posteriores. Puede configurarlo en Visual Studio en **Analizar** > **Portability Analyzer Settings** (Configuración del Analizador de portabilidad) y seleccionando las plataformas de destino, que son las plataformas y versiones de .NET en las que desea evaluar las brechas de portabilidad en comparación con la plataforma y versión con la que se ha creado el ensamblado actual.

![Captura de pantalla de la portabilidad](./media/portability-analyzer/portability-screenshot.png)

También puede usar la aplicación de consola ApiPort, descárguela desde [el repositorio de ApiPort](http://aka.ms/apiportdownload). Puede usar la opción de comando `listTargets` para mostrar la lista de destinos disponible y elegir las plataformas de destino especificando la opción de comando `-t` o `--target`. 

### <a name="analyze-portability"></a>Análisis de portabilidad
Para analizar todo el proyecto en Visual Studio, haga clic con el botón derecho en el proyecto en **Explorador de soluciones** y seleccione **Analyze Assembly Portability** (Analizar la portabilidad del ensamblado). También puede ir al menú **Analizar** y seleccionar **Analyze Assembly Portability** (Analizar la portabilidad del ensamblado). Desde allí, seleccione el ejecutable o .dll del proyecto.

![Analizador de portabilidad desde el Explorador de soluciones](./media/portability-analyzer/portability-solution-explorer.png)

También puede usar la [aplicación de consola ApiPort](https://aka.ms/apiportdownload). 

* Escriba el comando siguiente para analizar el directorio actual: `ApiPort.exe analyze -f .`
* Para analizar una lista específica de archivos .dll, escriba el comando siguiente: `ApiPort.exe analyze -f first.dll -f second.dll -f third.dll`
* Ejecute `ApiPort.exe -?` para obtener más ayuda.

Se recomienda que incluya todos los archivos exe y dll relacionados que posea y desea portar, y que excluya los archivos de los que depende la aplicación, pero que no posee y no puede portar. Esto le proporcionará un informe de portabilidad más relevante.  

### <a name="view-and-interpret-portability-result"></a>Vista e interpretación de los resultados de portabilidad

Solo las API que no son compatibles con una plataforma de destino aparecen en el informe. Después de ejecutar el análisis en Visual Studio, verá que aparecerá el vínculo del archivo de informe de portabilidad de .NET. Si ha usado la [aplicación de consola ApiPort](https://aka.ms/apiportdownload), el informe de portabilidad de .NET se guardará como archivo en el formato especificado. El valor predeterminado es en un archivo de Excel ( *.xlsx*) ubicado en el directorio actual.

#### <a name="portability-summary"></a>Resumen de portabilidad 

![Resumen de portabilidad](./media/portability-analyzer/portabilitysummary.png)

En la sección Resumen de portabilidad del informe se muestra el porcentaje de portabilidad para cada ensamblado incluido en la ejecución. En el ejemplo anterior, el 89,74 % de las API de .NET Framework utilizadas en la aplicación `ConsoleAppFramework` están disponibles en .NET Core + extensiones de la plataforma v2.2. Si ejecuta la herramienta Analizador de portabilidad de .NET en varios ensamblados, cada ensamblado debe tener una fila en el informe de Resumen de portabilidad.

#### <a name="details"></a>Detalles

![Detalles de portabilidad](./media/portability-analyzer/portabilitydetails.png)

La sección Detalles del informe enumera las API que faltan desde una de las plataformas de destino. 

 - Tipo de destino: al tipo le falta la API desde una plataforma de destino 
 - Miembro de destino: el método no está presente en una plataforma de destino 
 - Nombre del ensamblado: el ensamblado de .NET Framework en el que se encuentra la API que falta. 
 - Cada una de las plataformas de destino seleccionada es una columna, como ".NET Core": El valor de "No compatible" significa que la API no se admite en esta plataforma de destino. 
 - Cambios recomendados: API o tecnología recomendada a la que realizar el cambio. Actualmente, este campo está vacío o no está actualizado para muchas de las API. Debido a la gran cantidad de API, nos enfrentamos a gran desafío para mantenerlas actualizadas. Estamos examinando soluciones alternativas para proporcionar información útil a los clientes.

#### <a name="missing-assemblies"></a>Ensamblados que faltan

![Detalles de portabilidad](./media/portability-analyzer/missingassemblies.png)

Puede encontrar la sección Ensamblados que faltan en el informe. En él se indica que esta lista de ensamblados hace referencia a los ensamblados analizados y no analizados. Si se trata un ensamblado que posee, inclúyalo en la ejecución del analizador de portabilidad de API para que pueda obtener informe detallado de portabilidad a nivel de API. Si se trata de una biblioteca de terceros, busque si tienen la versión más reciente compatible con la plataforma de destino. Si es así, le recomendamos que migre a la versión más reciente. Finalmente, sería de esperar que esta lista incluya todos los ensamblados de terceros que dependen de la aplicación y confirmar que tienen una versión compatible con la plataforma de destino.  

Para obtener más información sobre el Analizador de portabilidad de .NET, visite la [documentación de GitHub](https://github.com/Microsoft/dotnet-apiport#documentation) y el vídeo de Channel 9 [A Brief Look at the .NET Portability Analyzer](https://channel9.msdn.com/Blogs/Seth-Juarez/A-Brief-Look-at-the-NET-Portability-Analyzer) (Información breve sobre el Analizador de portabilidad de .NET).


