---
title: Comando dotnet msbuild
description: El comando dotnet msbuild proporciona acceso a la línea de comandos de MSBuild.
ms.date: 12/03/2018
ms.openlocfilehash: 983fae6f4ecf875da0b155a668009984b5df50de
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632029"
---
# <a name="dotnet-msbuild"></a>dotnet msbuild

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>nombre

`dotnet msbuild`: compila un proyecto y todas sus dependencias.

## <a name="synopsis"></a>Sinopsis

`dotnet msbuild <msbuild_arguments> [-h]`

## <a name="description"></a>Descripción

El comando `dotnet msbuild` permite el acceso a una instancia de MSBuild completamente funcional.

El comando tiene exactamente las mismas funcionalidades que el cliente de línea de comandos de MSBuild existente solo para proyectos de tipo SDK. Las opciones son las mismas. Para obtener más información sobre las opciones disponibles, vea la [Referencia de la línea de comandos de MSBuild](/visualstudio/msbuild/msbuild-command-line-reference).

El comando [dotnet build](dotnet-build.md) es equivalente al comando `dotnet msbuild -restore -target:Build`. `dotnet build` suele utilizase para compilar proyectos, pero `dotnet msbuild` le aporta mayor control. Por ejemplo, si hay un destino concreto que quiere ejecutar (sin ejecutar el destino de compilación), probablemente prefiera usar `dotnet msbuild`.

## <a name="examples"></a>Ejemplos

* Creación de un proyecto y sus dependencias:

  ```console
  dotnet msbuild
  ```

* Creación de un proyecto y sus dependencias mediante la configuración de lanzamiento:

  ```console
  dotnet msbuild -p:Configuration=Release
  ```

* Ejecuta el destino de publicación y publica para el RID `osx.10.11-x64`:

  ```console
  dotnet msbuild -t:Publish -p:RuntimeIdentifiers=osx.10.11-x64
  ```

* Visualización del proyecto completo con todos los destinos incluidos en el SDK:

  ```console
  dotnet msbuild -pp
  ```
