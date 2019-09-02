---
title: Comando dotnet clean
description: El comando dotnet clean limpia el directorio actual.
ms.date: 06/26/2019
ms.openlocfilehash: 113bc076b9f14a471c631801fe4a7cb1e044a411
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168057"
---
# <a name="dotnet-clean"></a>dotnet clean

**Este tema se aplica a: ✓** SDK de .NET Core 1.x y versiones posteriores

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>nombre

`dotnet clean`: limpia la salida de un proyecto.

## <a name="synopsis"></a>Sinopsis

```console
dotnet clean [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--interactive] 
    [--nologo] [-o|--output] [-r|--runtime] [-v|--verbosity]
dotnet clean [-h|--help]
```

## <a name="description"></a>DESCRIPCIÓN

El comando `dotnet clean` limpia la salida de la compilación anterior. Se implementa como un [destino MSBuild](/visualstudio/msbuild/msbuild-targets), por lo que el proyecto se evalúa cuando se ejecuta el comando. Solo se limpian las salidas que se crearon durante la compilación. Se limpian las carpetas intermedias (*obj*) y de la salida final (*bin*).

## <a name="arguments"></a>Argumentos

`PROJECT | SOLUTION`

Proyecto o solución de MSBuild que se va a limpiar. Si no se especifica un archivo de proyecto o solución, MSBuild busca en el directorio de trabajo actual un archivo que tenga una extensión de archivo que termine en *proj* o *sln* y lo usa.

## <a name="options"></a>Opciones

* **`-c|--configuration {Debug|Release}`**

  Define la configuración de compilación. El valor predeterminado es `Debug`. Esta opción solo es necesaria al realizar la limpieza si la especificó durante el tiempo de compilación.

* **`-f|--framework <FRAMEWORK>`**

  El [marco](../../standard/frameworks.md) que se especificó en tiempo de compilación. El marco se debe definir en el [archivo de proyecto](csproj.md). Si especificó el marco en tiempo de compilación, debe especificar el marco al realizar la limpieza.

* **`-h|--help`**

  Imprime una corta ayuda para el comando.

* **`--interactive`**

  Permite que el comando se detenga y espere una entrada o una acción del usuario. Por ejemplo, para completar la autenticación. Disponible desde el SDK de .NET Core 3.0.

* **`--nologo`**

  No se muestra la pancarta de inicio ni el mensaje de copyright. Disponible desde el SDK de .NET Core 3.0.

* **`-o|--output <OUTPUT_DIRECTORY>`**

  Directorio que contiene los artefactos compilados que se van a limpiar. Especifique el modificador `-f|--framework <FRAMEWORK>` con el modificador del directorio de salida si especificó el marco cuando se compiló el proyecto.

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Limpia la carpeta de salida del tiempo de ejecución especificado. Esto se usa si se ha creado una [implementación autocontenida](../deploying/index.md#self-contained-deployments-scd). Opción disponible desde el SDK de .NET Core 2.0.

* **`-v|--verbosity <LEVEL>`**

  Establece el nivel de detalle de MSBuild. Los valores permitidos son `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` y `diag[nostic]`. De manera predeterminada, es `normal`.

## <a name="examples"></a>Ejemplos

* Limpie una compilación predeterminada del proyecto:

  ```console
  dotnet clean
  ```

* Limpie un proyecto creado con la configuración de lanzamiento:

  ```console
  dotnet clean --configuration Release
  ```
