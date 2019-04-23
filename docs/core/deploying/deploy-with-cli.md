---
title: Publicación de aplicaciones .NET Core con la CLI
description: Obtenga información sobre cómo publicar una aplicación .NET Core con las herramientas de la interfaz de la línea de comandos (CLI) del SDK de .NET Core.
author: thraka
ms.author: adegeo
ms.date: 01/16/2019
dev_langs:
- csharp
- vb
ms.custom: seodec18
ms.openlocfilehash: a72e5e557cd3aa098b674bffd277e3cc6da99d33
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59306071"
---
# <a name="publish-net-core-apps-with-the-cli"></a>Publicación de aplicaciones .NET Core con la CLI

En este artículo se muestra cómo se puede publicar la aplicación .NET Core desde la línea de comandos. .NET core proporciona tres maneras de publicar las aplicaciones. La implementación dependiente del marco de trabajo genera un archivo .dll multiplataforma que usa el runtime de .NET Core instalado localmente. La implementación dependiente del marco de trabajo genera un archivo ejecutable específico de la plataforma que usa el runtime de .NET Core instalado localmente. El archivo ejecutable independiente genera un archivo ejecutable específico de la plataforma e incluye una copia local del runtime de .NET Core.

Para obtener información general sobre estos modos de publicación, vea [Implementación de aplicaciones .NET Core](index.md).

¿Busca ayuda rápida sobre el uso de la CLI? En la tabla siguiente se muestran algunos ejemplos de cómo publicar la aplicación. La plataforma de destino se puede especificar con el parámetro `-f <TFM>` o si edita el archivo de proyecto. Para más información, vea [Conceptos básicos de publicación](#publishing-basics).

| Modo de publicación | Versión del SDK | Comando |
| ------------ | ----------- | ------- |
| Implementación dependiente de marco de trabajo | 2.x | `dotnet publish -c Release` |
| Archivo ejecutable dependiente de la plataforma | 2.2 | `dotnet publish -c Release -r <RID> --self-contained false` |
|                                | 3.0 | `dotnet publish -c Release -r <RID> --self-contained false` |
|                                | 3.0* | `dotnet publish -c Release` |
| Implementación autocontenida      | 2.1 | `dotnet publish -c Release -r <RID> --self-contained true` |
|                                | 2.2 | `dotnet publish -c Release -r <RID> --self-contained true` |
|                                | 3.0 | `dotnet publish -c Release -r <RID> --self-contained true` |

\* Si se usa el archivo ejecutable dependiente del marco de la versión 3.0 del SDK, se trata del modo de publicación predeterminado cuando se ejecuta el comando `dotnet publish` básico. Esto solo se aplica cuando el proyecto tiene como destino **.NET Core 2.1** o **.NET Core 3.0**.

## <a name="publishing-basics"></a>Conceptos básicos de publicación

El valor `<TargetFramework>` del archivo de proyecto especifica la plataforma de destino predeterminada al publicar la aplicación. Se puede cambiar la plataforma de destino a cualquier [moniker de la plataforma de destino (TFM)](../../standard/frameworks.md). Por ejemplo, si en el proyecto se usa `<TargetFramework>netcoreapp2.2</TargetFramework>`, se crea un archivo binario que tiene como destino .NET Core 2.2. El TFM especificado en esta configuración es el destino predeterminado que usa el comando [`dotnet publish`](../tools/dotnet-publish.md).

Si quiere tener como destino más de una plataforma, puede establecer el valor `<TargetFrameworks>` en más de un valor de TFM separados por punto y coma. Puede publicar una de las plataformas con el comando `dotnet publish -f <TFM>`. Por ejemplo, si tiene `<TargetFrameworks>netcoreapp2.1;netcoreapp2.2</TargetFrameworks>` y ejecuta `dotnet publish -f netcoreapp2.1`, se crea un archivo binario que tiene como destino .NET Core 2.1.

A menos que se establezca otro, el directorio de salida del comando [`dotnet publish`](../tools/dotnet-publish.md) es `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/`. El modo **BUILD-CONFIGURATION** predeterminado es **Depurar** a menos que se cambie con el parámetro `-c`. Por ejemplo, `dotnet publish -c Release -f netcoreapp2.1` publica en `myfolder/bin/Release/netcoreapp2.1/publish/`.

Si usa el SDK 3.0 de .NET Core, el modo de publicación predeterminado para las aplicaciones destinadas a las versiones 2.1, 2.2 y 3.0 de .NET Core es el ejecutable dependiente de la plataforma.

Si usa el SDK 2.1 de .NET Core, el modo de publicación predeterminado para las aplicaciones destinadas a las versiones 2.1 y 2.2 de .NET Core es la implementación dependiente de la plataforma.

### <a name="native-dependencies"></a>Dependencias nativas

Si la aplicación tiene dependencias nativas, es posible que no funcione en otro sistema operativo. Por ejemplo, si en la aplicación se usa la API Windows nativa, no se ejecutará en macOS o Linux. Tendrá que proporcionar código específico de la plataforma y compilar un archivo ejecutable para cada plataforma.

Tenga en cuenta también que, si una biblioteca a la que se hace referencia tiene una dependencia nativa, es posible que la aplicación no se ejecute en todas las plataformas. Pero es posible que un paquete NuGet al que se hace referencia incluya versiones específicas de la plataforma para controlar de forma automática las dependencias nativas necesarias.

Al distribuir una aplicación con dependencias nativas, es posible que tenga que usar el modificador `dotnet publish -r <RID>` para especificar la plataforma de destino para la que se quiere publicar. Para obtener una lista de identificadores de tiempo de ejecución, vea [Catálogo de identificadores de entorno de ejecución (RID) de .NET Core](../rid-catalog.md).

En las secciones [Archivo ejecutable dependiente de la plataforma](#framework-dependent-executable) e [Implementación autocontenida](#self-contained-deployment) se ofrece más información sobre los archivos binarios específicos de la plataforma.

## <a name="sample-app"></a>Aplicación de ejemplo

Puede usar la siguiente aplicación de ejemplo para explorar los comandos de publicación. La aplicación se crea mediante la ejecución de los comandos siguientes en el terminal:

```dotnetcli
mkdir apptest1
cd apptest1
dotnet new console
dotnet add package Figgle
```

Es necesario cambiar el archivo `Program.cs` o `Program.vb` que genera la plantilla de consola por lo siguiente:

```csharp
using System;

namespace apptest1
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"));
        }
    }
}
```

```vb
Imports System

Module Program
    Sub Main(args As String())
        Console.WriteLine(Figgle.FiggleFonts.Standard.Render("Hello, World!"))
    End Sub
End Module
```

Al ejecutar la aplicación ([`dotnet run`](../tools/dotnet-run.md)), se muestra el resultado siguiente:

```terminal
  _   _      _ _         __        __         _     _ _
 | | | | ___| | | ___    \ \      / /__  _ __| | __| | |
 | |_| |/ _ \ | |/ _ \    \ \ /\ / / _ \| '__| |/ _` | |
 |  _  |  __/ | | (_) |    \ V  V / (_) | |  | | (_| |_|
 |_| |_|\___|_|_|\___( )    \_/\_/ \___/|_|  |_|\__,_(_)
                     |/
```

## <a name="framework-dependent-deployment"></a>Implementación dependiente de marco de trabajo

Para la CLI del SDK de .NET Core 2.x, la implementación dependiente de la plataforma (FDD) es el modo predeterminado para el comando `dotnet publish` básico.

Cuando la aplicación se publica como una FDD, se crea un archivo `<PROJECT-NAME>.dll` en la carpeta `./bin/<BUILD-CONFIGURATION>/<TFM>/publish/`. Para ejecutar la aplicación, vaya a la carpeta de salida y use el comando `dotnet <PROJECT-NAME>.dll`.

La aplicación está configurada para tener como destino una versión específica de .NET Core. Es obligatorio que ese runtime de .NET Core de destino esté en el equipo donde se quiere ejecutar la aplicación. Por ejemplo, si la aplicación tiene como destino .NET Core 2.2, todos los equipos en los que se ejecute la aplicación deben tener instalado el runtime de .NET Core 2.2. Como se indica en la sección [Conceptos básicos de publicación](#publishing-basics), se puede editar el archivo de proyecto para cambiar la plataforma de destino predeterminada o seleccionar más de una como destino.

Al publicar una FDD se crea una aplicación que realiza la puesta al día automática a la revisión de seguridad de .NET Core más reciente disponible en el sistema en el que se ejecuta la aplicación. Para más información sobre el enlace de versión en tiempo de compilación, vea [Selección de la versión de .NET Core que se va a usar](../versions/selection.md#framework-dependent-apps-roll-forward).

## <a name="framework-dependent-executable"></a>Archivo ejecutable dependiente de la plataforma

Para la CLI del SDK de .NET Core 3.x, el archivo ejecutable dependiente de la plataforma (FDE) es el modo predeterminado para el comando `dotnet publish` básico. No es necesario especificar ningún otro parámetro, siempre que se quiera establecer como destino el sistema operativo actual.

En este modo, se crea un host ejecutable específico de la plataforma para hospedar la aplicación multiplataforma. Este modo es similar a FDD ya requiere un host en forma del comando `dotnet`. El nombre de archivo ejecutable de host varía según la plataforma y es similar a `<PROJECT-FILE>.exe`. Este archivo ejecutable se puede ejecutar directamente en lugar de llamar a `dotnet <PROJECT-FILE>.dll`, que sigue siendo una forma aceptable de ejecutar la aplicación.

La aplicación está configurada para tener como destino una versión específica de .NET Core. Es obligatorio que ese runtime de .NET Core de destino esté en el equipo donde se quiere ejecutar la aplicación. Por ejemplo, si la aplicación tiene como destino .NET Core 2.2, todos los equipos en los que se ejecute la aplicación deben tener instalado el runtime de .NET Core 2.2. Como se indica en la sección [Conceptos básicos de publicación](#publishing-basics), se puede editar el archivo de proyecto para cambiar la plataforma de destino predeterminada o seleccionar más de una como destino.

Al publicar un FDE se crea una aplicación que realiza la puesta al día automática a la revisión de seguridad de .NET Core más reciente disponible en el sistema en el que se ejecuta la aplicación. Para más información sobre el enlace de versión en tiempo de compilación, vea [Selección de la versión de .NET Core que se va a usar](../versions/selection.md#framework-dependent-apps-roll-forward).

Excepto para .NET Core 3.x cuando el destino es la plataforma actual, se deben usar los siguientes modificadores con el comando `dotnet publish` para publicar un FDE:

- `-r <RID>` Este modificador usa un identificador (RID) para especificar la plataforma de destino. Para obtener una lista de identificadores de tiempo de ejecución, vea [Catálogo de identificadores de entorno de ejecución (RID) de .NET Core](../rid-catalog.md).

- `--self-contained false` Este modificador indica al SDK de .NET Core que cree un archivo ejecutable como un FDE.

Siempre que se usa el modificador `-r`, la ruta de acceso de la carpeta de salida cambia a: `./bin/<BUILD-CONFIGURATION>/<TFM>/<RID>/publish/`

Si usa la [aplicación de ejemplo](#sample-app), ejecute `dotnet publish -f netcoreapp2.2 -r win10-x64 --self-contained false`. Este comando crea el archivo ejecutable siguiente: `./bin/Debug/netcoreapp2.2/win10-x64/publish/apptest1.exe`

> [!NOTE]
> Puede reducir el tamaño total de la implementación si habilita el **modo de globalización invariable**. Este modo es útil para las aplicaciones que no son globales y que pueden usar las convenciones de formato, las de mayúsculas y minúsculas, y el criterio de ordenación y la comparación de cadenas de la [referencia cultural invariable](xref:System.Globalization.CultureInfo.InvariantCulture). Para más información sobre el **modo de globalización invariable** y cómo habilitarlo, vea [.NET Core Globalization Invariant Mode](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/globalization-invariant-mode.md) (Modo de globalización invariable de .NET Core).

## <a name="self-contained-deployment"></a>Implementación autocontenida

Cuando se publica una implementación autocontenida (SCD), el SDK de .NET Core crea un archivo ejecutable específico de la plataforma. La publicación de una SCD incluye todos los archivos de .NET Core necesarios para ejecutar la aplicación, pero no incluye las [dependencias nativas de .NET Core](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md). Estas dependencias deben estar presentes en el sistema antes de ejecutar la aplicación.

Al publicar una SCD, se crea una aplicación que no se pone al día a la revisión de seguridad de .NET Core más reciente disponible. Para más información sobre el enlace de versión en tiempo de compilación, vea [Selección de la versión de .NET Core que se va a usar](../versions/selection.md#self-contained-deployments-include-the-selected-runtime).

Debe usar los modificadores siguientes con el comando `dotnet publish` para publicar una SCD:

- `-r <RID>` Este modificador usa un identificador (RID) para especificar la plataforma de destino. Para obtener una lista de identificadores de tiempo de ejecución, vea [Catálogo de identificadores de entorno de ejecución (RID) de .NET Core](../rid-catalog.md).

- `--self-contained true` Este modificador indica al SDK de .NET Core que cree un archivo ejecutable como una SCD.

> [!NOTE]
> Puede reducir el tamaño total de la implementación si habilita el **modo de globalización invariable**. Este modo es útil para las aplicaciones que no son globales y que pueden usar las convenciones de formato, las de mayúsculas y minúsculas, y el criterio de ordenación y la comparación de cadenas de la [referencia cultural invariable](xref:System.Globalization.CultureInfo.InvariantCulture). Para más información sobre el **modo de globalización invariable** y cómo habilitarlo, vea [.NET Core Globalization Invariant Mode](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/globalization-invariant-mode.md) (Modo de globalización invariable de .NET Core).

## <a name="see-also"></a>Vea también

- [Información general sobre la implementación de aplicaciones .NET Core](index.md)
- [Catálogo de identificadores de entorno de ejecución (RID) de .NET Core](../rid-catalog.md)
