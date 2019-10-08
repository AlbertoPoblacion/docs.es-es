---
title: Organización de proyectos para .NET Framework y .NET Core
description: Ayuda para los propietarios del proyecto que quieren compilar su solución en .NET Framework y en .NET Core, en paralelo.
author: conniey
ms.date: 12/07/2018
ms.custom: seodec18
ms.openlocfilehash: 1e120e1aee60e88ea33a8290f3bf36eb93bfc91c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698934"
---
# <a name="organize-your-project-to-support-both-net-framework-and-net-core"></a>Organización del proyecto para admitir .NET Framework y .NET Core

Aprenda a crear una solución que se compila para .NET Framework y .NET Core en paralelo. Consulte varias opciones para organizar los proyectos para alcanzar este objetivo. Los siguientes son algunos escenarios típicos que debe considerar cuando decida cómo va a configurar el diseño del proyecto con .NET Core. Es posible que la lista no abarque todos los aspectos que quiere, pero debe darles prioridad en función de las necesidades del proyecto.

* [**Combinar los proyectos existentes y los proyectos de .NET Core en proyectos únicos**](#replace-existing-projects-with-a-multi-targeted-net-core-project)

  *Para qué se usa:*
  * Para simplificar el proceso de compilación mediante la compilación de un proyecto único en lugar de compilar varios proyectos, donde cada uno de ellos tiene como destino una plataforma o versión distinta de .NET Framework.
  * Simplifique la administración de archivos de origen en proyectos con compatibilidad con múltiples versiones, porque debe administrar un solo archivo de proyecto. Cuando agrega o quita archivos de origen, las alternativas requieren que los sincronice manualmente con los otros proyectos.
  * Para generar fácilmente un paquete NuGet para consumo.
  * Le permite escribir código para una versión específica de .NET Framework en las bibliotecas a través del uso de directivas de compilador.

  *Escenarios no admitidos:*
  * Se necesita que los desarrolladores que usan Visual Studio 2017 abran los proyectos existentes. Para admitir versiones anteriores de Visual Studio, una opción mejor es [mantener los archivos de proyecto en distintas carpetas](#support-vs).

* <a name="support-vs"></a>[**Mantener separados los proyectos existentes y los proyectos de .NET Core nuevos**](#keep-existing-projects-and-create-a-net-core-project)

  *Para qué se usa:*
  * Para mantener la compatibilidad con el desarrollo en proyectos existentes sin tener que hacer una actualización para los desarrolladores o colaboradores que posiblemente no tengan Visual Studio 2017.
  * Para disminuir la posibilidad de generar nuevos errores en proyectos existentes porque esos proyectos no requieren renovación de código.

## <a name="example"></a>Ejemplo

Considere el siguiente repositorio:

![Proyecto existente](./media/project-structure/existing-project-structure.png)

[**Código fuente**](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library/)

A continuación se describen varias formas de agregar compatibilidad para .NET Core para este repositorio en función de las restricciones y la complejidad de los proyectos existentes.

## <a name="replace-existing-projects-with-a-multi-targeted-net-core-project"></a>Reemplazo de proyectos existentes por un proyecto .NET Core con compatibilidad con múltiples versiones

Reorganice el repositorio de manera que se quite cualquier archivo *\*.csproj* existente y se cree un archivo *\*.csproj* único que establezca varios marcos de trabajo como destino. Esta es una opción excelente, porque un proyecto único se puede compilar para distintos marcos de trabajo. También tiene la capacidad de controlar distintas dependencias y opciones de compilación por cada marco de trabajo de destino.

![Creación de un csproj con varios marcos de destino](./media/project-structure/multi-targeted-project.png)

[**Código fuente**](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library-csproj/)

Los cambios que debe tener en cuenta son los siguientes:

* Se reemplazan *packages.config* y *\*.csproj* con un nuevo archivo [ *\*.csproj*](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library-csproj/src/Car/Car.csproj) de .NET Core. Los paquetes NuGet se especifican con `<PackageReference> ItemGroup`.

## <a name="keep-existing-projects-and-create-a-net-core-project"></a>Mantenimiento de los proyectos existentes y creación de un proyecto .NET Core

Si hay proyectos existentes que tienen como destino marcos de trabajo anteriores, puede que desee dejarlos intactos y usar un proyecto .NET Core para establecer como destino marcos de trabajo futuros.

![Proyecto .NET Core con un proyecto existente en otra carpeta](./media/project-structure/separate-projects-same-source.png)

[**Código fuente**](https://github.com/dotnet/samples/tree/master/framework/libraries/migrate-library-csproj-keep-existing/)

Los cambios que debe tener en cuenta son los siguientes:

* .NET Core y los proyectos existentes se mantienen en carpetas independientes.
  * Mantener los proyectos en carpetas independientes evita que sea necesario tener Visual Studio 2017. Puede crear una solución independiente que solo abra los proyectos anteriores.

## <a name="see-also"></a>Vea también

- [Documentación sobre la portabilidad a .NET Core](index.md)
