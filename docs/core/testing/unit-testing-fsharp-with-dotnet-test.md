---
title: Prueba unitaria de F# en .NET Core con dotnet test y xUnit
description: 'Aprenda los conceptos de pruebas unitarias para F# en .NET Core: cree paso a paso una solución de ejemplo mediante pruebas de dotnet y xUnit.'
author: billwagner
ms.author: wiwagn
ms.date: 08/30/2017
ms.custom: seodec18
ms.openlocfilehash: 3a9744bfebd93c5004011819b8c6e739e84b97d0
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68626492"
---
# <a name="unit-testing-f-libraries-in-net-core-using-dotnet-test-and-xunit"></a>Bibliotecas de F# de prueba unitaria en .NET Core con pruebas de dotnet y xUnit

Este tutorial le guía por una experiencia interactiva de creación de una solución de ejemplo paso a paso para aprender los conceptos de pruebas unitarias. Si prefiere seguir el tutorial con una solución precompilada, [vea o descargue el código de ejemplo](https://github.com/dotnet/samples/tree/master/core/getting-started/unit-testing-with-fsharp/) antes de comenzar. Para obtener instrucciones de descarga, vea [Ejemplos y tutoriales](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

## <a name="creating-the-source-project"></a>Crear el proyecto de origen

Abra una ventana del Shell. Cree un directorio llamado *unit-testing-with-fsharp* que contenga la solución.
En este directorio nuevo, ejecute [`dotnet new sln`](../tools/dotnet-new.md) para crear una solución nueva. Esto permite facilitar la administración de la biblioteca de clases y del proyecto de prueba unitaria.
En el directorio de la solución, cree un directorio *MathService*. Esta es la estructura de directorios y archivos hasta el momento:

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
```

Make *MathService* the current directory and run [`dotnet new classlib -lang F#`](../tools/dotnet-new.md) to create the source project.  Creará una implementación de errores del servicio de matemáticas:

```fsharp
module MyMath =
    let squaresOfOdds xs = raise (System.NotImplementedException("You haven't written a test yet!"))
```

Cambie nuevamente el directorio al directorio *unit-testing-with-fsharp*. Ejecute [`dotnet sln add .\MathService\MathService.fsproj`](../tools/dotnet-sln.md) para agregar el proyecto de biblioteca de clases a la solución.

## <a name="creating-the-test-project"></a>Crear el proyecto de prueba

A continuación, cree el directorio *MathService.Tests*. En el esquema siguiente se muestra la estructura de directorios:

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
```

Convierta el directorio *MathService.Tests* en el directorio actual y cree un proyecto nuevo con [`dotnet new xunit -lang F#`](../tools/dotnet-new.md). Esto crea un proyecto de prueba que usa xUnit como biblioteca de pruebas. La plantilla generada configura el ejecutor de pruebas en *MathServiceTests.fsproj*:

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="15.3.0-preview-20170628-02" />
  <PackageReference Include="xunit" Version="2.2.0" />
  <PackageReference Include="xunit.runner.visualstudio" Version="2.2.0" />
</ItemGroup>
```

El proyecto de prueba requiere otros paquetes para crear y ejecutar pruebas unitarias. `dotnet new` en el paso anterior, agregó xUnit y el ejecutor de xUnit. Ahora, agregue la biblioteca de clases `MathService` como otra dependencia al proyecto. Use el comando [`dotnet add reference`](../tools/dotnet-add-reference.md):

```
dotnet add reference ../MathService/MathService.fsproj
```

Puede ver todo el archivo en el [repositorio de muestras](https://github.com/dotnet/samples/blob/master/core/getting-started/unit-testing-with-fsharp/MathService.Tests/MathService.Tests.fsproj) en GitHub.

Tiene el diseño de solución final siguiente:

```
/unit-testing-with-fsharp
    unit-testing-with-fsharp.sln
    /MathService
        Source Files
        MathService.fsproj
    /MathService.Tests
        Test Source Files
        MathServiceTests.fsproj
```

Ejecute [`dotnet sln add .\MathService.Tests\MathService.Tests.fsproj`](../tools/dotnet-sln.md) en el directorio *unit-testing-with-fsharp*. 

## <a name="creating-the-first-test"></a>Crear la primera prueba

Escribirá una prueba de errores, la aprobará y, luego, repetirá el proceso. Abra *Tests.fs* y agregue el código siguiente:

```fsharp
[<Fact>]
let ``My test`` () =
    Assert.True(true)

[<Fact>]
let ``Fail every time`` () = Assert.True(false)
```

El atributo `[<Fact>]` indica un método de prueba que el ejecutor de pruebas ejecuta. En *unit-testing-with-fsharp*, ejecute [`dotnet test`](../tools/dotnet-test.md) para compilar las pruebas y la biblioteca de clases y luego ejecutar las pruebas. El ejecutor de pruebas de xUnit tiene el punto de entrada del programa para ejecutar las pruebas desde la consola. `dotnet test` inicia el ejecutor de pruebas con el proyecto de prueba unitaria que creó.

Estas dos pruebas muestran las pruebas superadas y con errores más básicas. `My test` indica que se supera y `Fail every time` indica que no. Ahora, cree una prueba para el método `squaresOfOdds`. El método `squaresOfOdds` devuelve una secuencia de los cuadrados de todos los valores enteros impares que forman parte de la secuencia de entrada. En lugar de intentar escribir todas esas funciones a la vez, puede crear de forma iterativa pruebas que validen la funcionalidad. Hacer cada prueba superada significa crear la funcionalidad necesaria para el método.

La prueba más sencilla que se puede escribir es llamar a `squaresOfOdds` con todos los números impares, donde el resultado sea una secuencia de enteros vacía.  Aquí se muestra la prueba:

```fsharp
[<Fact>]
let ``Sequence of Evens returns empty collection`` () =
    let expected = Seq.empty<int>
    let actual = MyMath.squaresOfOdds [2; 4; 6; 8; 10]
    Assert.Equal<Collections.Generic.IEnumerable<int>>(expected, actual)
```

La prueba produce un error. Todavía no ha creado la implementación. Cree esta prueba que se supera escribiendo el código más simple en la clase `MathService` que funciona:

```fsharp
let squaresOfOdds xs =
    Seq.empty<int>
```

En el directorio *unit-testing-with-fsharp*, vuelva a ejecutar `dotnet test`. El comando `dotnet test` ejecuta una compilación del proyecto `MathService` y luego del proyecto `MathService.Tests`. Después de compilar ambos proyectos, se ejecuta esta única prueba. Pasa.

## <a name="completing-the-requirements"></a>Finalización de los requisitos

Ahora que la prueba se ha superado, es el momento de escribir más. El próximo caso simple funciona con una secuencia cuyo único número impar es `1`. El número 1 es más simple, porque el cuadrado de 1 es 1. Aquí está la prueba siguiente:

```fsharp
[<Fact>]
let ``Sequences of Ones and Evens returns Ones`` () =
    let expected = [1; 1; 1; 1]
    let actual = MyMath.squaresOfOdds [2; 1; 4; 1; 6; 1; 8; 1; 10]
    Assert.Equal<Collections.Generic.IEnumerable<int>>(expected, actual)
```

La ejecución de `dotnet test` ejecuta las pruebas y muestra que la prueba nueva no se supera. Ahora actualice el método `squaresOfOdds` para controlar esta prueba nueva. Filtre todos los números impares y quítelos de la secuencia para que se supere esta prueba. Para hacerlo, escriba una función de filtro pequeña y use `Seq.filter`:

```fsharp
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs =
    xs
    |> Seq.filter isOdd
```

Falta un paso todavía: el cuadrado de cada uno de los números impares. Comience escribiendo una prueba nueva:

```fsharp
[<Fact>]
let ``SquaresOfOdds works`` () =
    let expected = [1; 9; 25; 49; 81]
    let actual = MyMath.squaresOfOdds [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]
    Assert.Equal(expected, actual)
```

Puede corregir la prueba si canaliza la secuencia filtrada a través de una operación de asignación para calcular el cuadrado de cada número impar:

```fsharp
let private square x = x * x
let private isOdd x = x % 2 <> 0

let squaresOfOdds xs = 
    xs 
    |> Seq.filter isOdd 
    |> Seq.map square
```

Ha creado una biblioteca pequeña y un conjunto de pruebas unitarias para esa biblioteca. Ha estructurado la solución, por lo que agregar pruebas y paquetes nuevos es parte del flujo de trabajo normal. Ha centrado la mayor parte del tiempo y del esfuerzo en resolver los objetivos de la aplicación.
