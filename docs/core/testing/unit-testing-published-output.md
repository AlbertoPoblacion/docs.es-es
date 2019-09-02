---
title: Prueba de la salida publicada con vstest dotnet
description: Obtenga información sobre cómo ejecutar pruebas en bibliotecas publicadas en lugar de código fuente, con el comando dotnet vstest.
author: kendrahavens
ms.author: kehavens
ms.date: 10/18/2017
ms.custom: seodec18
ms.openlocfilehash: 9ac03053bc762d0176e087545871ca8a145cd41e
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168290"
---
# <a name="test-published-output-with-dotnet-vstest"></a>Prueba de la salida publicada con vstest dotnet

Puede ejecutar pruebas en la salida ya publicada mediante el comando `dotnet vstest`. Esto funcionará en pruebas de xUnit, MSTest y NUnit. Simplemente busque el archivo DLL que formaba parte de la salida publicada y ejecute:

```console
dotnet vstest <MyPublishedTests>.dll
```

donde `<MyPublishedTests>` es el nombre del proyecto de prueba publicado.

## <a name="example"></a>Ejemplo

Los comandos siguientes muestran la ejecución de pruebas en un archivo DLL publicado.

```console
dotnet new mstest -o MyProject.Tests
cd MyProject.Tests
dotnet publish -o out
dotnet vstest out/MyProject.Tests.dll
```

> [!NOTE]
> Nota: Si la aplicación tiene como destino un marco distinto de `netcoreapp` todavía puede ejecutar el comando `dotnet vstest` si pasa el marco de destino con una marca de marco. Por ejemplo: `dotnet vstest <MyPublishedTests>.dll  --Framework:".NETFramework,Version=v4.6"`. En Visual Studio 2017 Update 5, se detecta automáticamente el marco deseado.

## <a name="see-also"></a>Vea también

- [Pruebas unitarias con pruebas de dotnet y xUnit](unit-testing-with-dotnet-test.md)
- [Prueba unitaria de C# con NUnit y .NET Core](unit-testing-with-nunit.md)
- [Pruebas unitarias con pruebas de dotnet y MSTest](unit-testing-with-mstest.md)
