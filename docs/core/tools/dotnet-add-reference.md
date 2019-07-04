---
title: Comando dotnet-add reference
description: El comando dotnet add reference constituye una opción práctica para agregar referencias entre proyectos.
ms.date: 06/26/2019
ms.openlocfilehash: 6e0ca40e701b62dcc18147f9de83cafa6aa2f50f
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67422001"
---
# <a name="dotnet-add-reference"></a>dotnet-add reference

**Este artículo se aplica a: ✓** SDK de .NET Core 1.x y versiones posteriores

<!-- todo: uncomment when all CLI commands are reviewed
[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]
-->

## <a name="name"></a>nombre

`dotnet add reference` Agrega referencias entre proyectos (P2P) .

## <a name="synopsis"></a>Sinopsis

`dotnet add [<PROJECT>] reference [-f|--framework] <PROJECT_REFERENCES> [-h|--help] [--interactive]`

## <a name="description"></a>Descripción

El comando `dotnet add reference` constituye una opción práctica para agregar referencias de proyecto a un proyecto. Después de ejecutar el comando, los elementos [`<ProjectReference>`](/visualstudio/msbuild/common-msbuild-project-items) se agregan al archivo del proyecto.

```xml
<ItemGroup>
  <ProjectReference Include="app.csproj" />
  <ProjectReference Include="..\lib2\lib2.csproj" />
  <ProjectReference Include="..\lib1\lib1.csproj" />
</ItemGroup>
```

## <a name="arguments"></a>Argumentos

* **`PROJECT`**

  Especifica el archivo del proyecto. Si no se especifica, el comando busca uno en el directorio actual.

* **`PROJECT_REFERENCES`**

  Referencias entre proyectos (P2P) que se van a agregar. Especifique uno o más proyectos. [El patrón glob](https://en.wikipedia.org/wiki/Glob_(programming)) se admite en sistemas basados en Unix/Linux.

## <a name="options"></a>Opciones

* **`-h|--help`**

  Imprime una corta ayuda para el comando.

* **`-f|--framework <FRAMEWORK>`**

  Agrega referencias de proyecto solo cuando apunta a un[marco](../../standard/frameworks.md) específico.

* **`--interactive`**

  Permite que el comando se detenga y espere la entrada o acción del usuario (por ejemplo, completar la autenticación). Disponible desde el SDK de .NET Core 3.0.

## <a name="examples"></a>Ejemplos

* Agregar una referencia de proyecto:

  ```console
  dotnet add app/app.csproj reference lib/lib.csproj
  ```

* Agregar varias referencias de proyecto al proyecto en el directorio actual:

  ```console
  dotnet add reference lib1/lib1.csproj lib2/lib2.csproj
  ```

* Agregar varias referencias de proyecto usando el patrón global en Linux/Unix:

  ```console
  dotnet add app/app.csproj reference **/*.csproj
  ```
