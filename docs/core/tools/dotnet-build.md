---
title: Comando dotnet build
description: El comando dotnet build compila un proyecto y todas sus dependencias.
ms.date: 04/24/2019
ms.openlocfilehash: 6564aacbe520797b47095929cfe72c6b180b99a7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632131"
---
# <a name="dotnet-build"></a>dotnet build

**Este artículo se aplica a: ✓** SDK de .NET Core 1.x y versiones posteriores

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>nombre

`dotnet build`: compila un proyecto y todas sus dependencias.

## <a name="synopsis"></a>Sinopsis

```
dotnet build [<PROJECT>|<SOLUTION>] [-c|--configuration] [-f|--framework] [--force] [--interactive] [--no-dependencies]
    [--no-incremental] [--nologo] [--no-restore] [-o|--output] [-r|--runtime] [-v|--verbosity] [--version-suffix]

dotnet build [-h|--help]
```

## <a name="description"></a>Descripción

El comando `dotnet build` crea el proyecto y sus dependencias en un conjunto de archivos binarios. Los archivos binarios incluyen el código del proyecto en archivos de lenguaje intermedio (IL) con una extensión *.dll* y los archivos de símbolos usados para la depuración con una extensión *.pdb*. Se genera un archivo JSON de dependencias (*\*. deps.json*) que incluye las dependencias de la aplicación. Se genera un archivo *\*.runtimeconfig.json*, que especifica el tiempo de ejecución compartido y su versión de la aplicación.

Si el proyecto tiene dependencias de terceros, como bibliotecas de NuGet, estas se resuelven desde la caché de NuGet y no están disponibles en la salida compilada del proyecto. Teniendo eso en cuenta, el producto de `dotnet build` no está listo para transferirse a otra máquina para ejecutarse. Esto contrasta con el comportamiento de .NET Framework en el que al compilar un proyecto ejecutable (una aplicación) se genera ese ejecutable en cualquier máquina donde esté instalado .NET. Para tener una experiencia similar con .NET Core, es necesario usar el comando [dotnet publish](dotnet-publish.md). Para obtener más información, consulte el tema [Implementación de aplicaciones .NET Core](../deploying/index.md).

La compilación requiere el archivo *project.assets.json*, que muestra las dependencias de la aplicación. El archivo se crea cuando se ejecuta [`dotnet restore`](dotnet-restore.md). Sin el archivo de recursos en su lugar, las herramientas no pueden resolver los ensamblados de referencia, lo que se traduce en errores. Con el SDK de .NET Core 1.x, era necesario ejecutar de forma explícita `dotnet restore` antes de ejecutar `dotnet build`. A partir del SDK de .NET Core 2.0, `dotnet restore` se ejecuta implícitamente al ejecutar `dotnet build`. Si quiere deshabilitar la restauración implícita cuando se ejecuta el comando de compilación, puede usar la opción `--no-restore`.

[!INCLUDE[dotnet restore note + options](~/includes/dotnet-restore-note-options.md)]

Si el proyecto es ejecutable o no viene determinado por la propiedad `<OutputType>` en el archivo del proyecto. En el ejemplo siguiente se muestra un proyecto en el que se genera código ejecutable:

```xml
<PropertyGroup>
  <OutputType>Exe</OutputType>
</PropertyGroup>
```

Para generar una biblioteca, omita la propiedad `<OutputType>`. La principal diferencia en la salida compilada es que la DLL de IL para una biblioteca no contiene puntos de entrada y no se puede ejecutar.

### <a name="msbuild"></a>MSBuild

`dotnet build` usa MSBuild para compilar el proyecto, por lo que admite las compilaciones en paralelo e incrementales. Para obtener más información, consulte [Compilaciones incrementales](/visualstudio/msbuild/incremental-builds).

Además de sus opciones, el comando `dotnet build` acepta opciones de MSBuild, como `-p` para establecer propiedades o `-l` para definir un registrador. Para obtener más información sobre estas opciones, vea la [Referencia de la línea de comandos de MSBuild](/visualstudio/msbuild/msbuild-command-line-reference). O también puede usar el comando [dotnet msbuild](dotnet-msbuild.md).

La ejecución de `dotnet build` es equivalente a `dotnet msbuild -restore -target:Build`.

## <a name="arguments"></a>Argumentos

`PROJECT | SOLUTION`

El archivo de proyecto o solución para compilar. Si no se especifica un archivo de proyecto o solución, MSBuild busca en el directorio de trabajo actual un archivo que tiene una extensión de archivo que termina por *proj* o *sln* y usa ese archivo.

## <a name="options"></a>Opciones

* **`-c|--configuration {Debug|Release}`**

  Define la configuración de compilación. El valor predeterminado es `Debug`.

* **`-f|--framework <FRAMEWORK>`**

  Compila para un [marco de trabajo](../../standard/frameworks.md) específico. El marco se debe definir en el [archivo de proyecto](csproj.md).

* **`--force`**

  Fuerza la resolución de todas las dependencias, incluso si la última restauración se realizó correctamente. Especificar esta marca es lo mismo que eliminar el archivo *project.assets.json*. Disponible a partir del SDK de .NET Core 2.0.

* **`-h|--help`**

  Imprime una corta ayuda para el comando.

* **`--interactive`**

  Permite que el comando se detenga y espere una entrada o una acción del usuario. Por ejemplo, para completar la autenticación. Disponible desde el SDK de .NET Core 3.0.

* **`--no-dependencies`**

  Omite las referencias de proyecto a proyecto (P2P) y solo compila el proyecto raíz especificado.

* **`--no-incremental`**

  Marca la compilación como no segura para la compilación incremental. Esta marca desactiva la compilación incremental y fuerza una recompilación limpia del gráfico de dependencias del proyecto.

* **`--no-logo`**

  No se muestra la pancarta de inicio ni el mensaje de copyright. Disponible desde el SDK de .NET Core 3.0.

* **`--no-restore`**

  No ejecuta una restauración implícita durante la compilación. Disponible a partir del SDK de .NET Core 2.0.

* **`-o|--output <OUTPUT_DIRECTORY>`**

  Directorio donde se colocan los archivos binarios compilados. También debe definir `--framework` cuando se especifica esta opción. Si no se especifica la ruta de acceso predeterminada es `./bin/<configuration>/<framework>/`.

* **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Especifica el tiempo de ejecución de destino. Para obtener una lista de identificadores de tiempo de ejecución (RID), consulte el [catálogo de RID](../rid-catalog.md).

* **`-v|--verbosity <LEVEL>`**

  Establece el nivel de detalle de MSBuild. Los valores permitidos son `q[uiet]`, `m[inimal]`, `n[ormal]`, `d[etailed]` y `diag[nostic]`. De manera predeterminada, es `minimal`.

* **`--version-suffix <VERSION_SUFFIX>`**

  Establece el valor de la propiedad `$(VersionSuffix)` que se va a usar al compilar el proyecto. Solo funciona si no se establece la propiedad `$(Version)`. A continuación, `$(Version)` se establece en `$(VersionPrefix)` combinada con `$(VersionSuffix)`, separadas por un guion.

## <a name="examples"></a>Ejemplos

* Creación de un proyecto y sus dependencias:

  ```console
  dotnet build
  ```

* Creación de un proyecto y sus dependencias mediante la configuración de lanzamiento:

  ```console
  dotnet build --configuration Release
  ```

* Compilación de un proyecto y sus dependencias para un tiempo de ejecución concreto (en este ejemplo, Ubuntu 18.04):

  ```console
  dotnet build --runtime ubuntu.18.04-x64
  ```

* Compile el proyecto y use origen del paquete NuGet especificado durante la operación de restauración (SDK de .NET Core 2.0 y versiones posteriores):

  ```console
  dotnet build --source c:\packages\mypackages
  ```

* Compile el proyecto y establezca la versión 1.2.3.4 como un parámetro de compilación:

  ```console
  dotnet build -p:Version=1.2.3.4
  ```
