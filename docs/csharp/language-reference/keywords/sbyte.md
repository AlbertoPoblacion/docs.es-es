---
title: 'sbyte: Referencia de C#'
ms.custom: seodec18
ms.date: 03/14/2017
f1_keywords:
- sbyte_CSharpKeyword
- sbyte
helpviewer_keywords:
- sbyte keyword [C#]
ms.assetid: 1a9c7b48-73d1-4d33-b485-c4faf0a816bc
ms.openlocfilehash: 124ff282fc354699c68e0a17c64f911db2e25869
ms.sourcegitcommit: 462dc41a13942e467984e48f4018d1f79ae67346
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "58185524"
---
# <a name="sbyte-c-reference"></a>sbyte (Referencia de C#)

`sbyte` denota un tipo entero que almacena valores según el tamaño y el intervalo que se indican en la tabla siguiente.

|Tipo|Intervalo|Tamaño|Tipo de .NET|
|----------|-----------|----------|-------------------------|
|`sbyte`|De -128 a 127|Entero de 8 bits con signo|<xref:System.SByte?displayProperty=nameWithType>|

## <a name="literals"></a>Literales

Puede declarar e inicializar una variable `sbyte` mediante la asignación de un literal decimal, un literal hexadecimal o (a partir de C# 7.0) un literal binario.

En el ejemplo siguiente, los enteros que equivalen a -102 que se representan como literales binarios, hexadecimales y decimales se convierten de [int](../../../csharp/language-reference/keywords/int.md) a valores `sbyte`.

[!code-csharp[SByte](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#SByte)]

> [!NOTE]
> Use el prefijo `0x` o `0X` para denotar un literal hexadecimal y el prefijo `0b` o `0B` para denotar un literal binario. Los literales decimales no tienen prefijo.

A partir de C# 7.0, se han agregado un par de características para mejorar la legibilidad.
- C# 7.0 permite usar el carácter de subrayado, `_`, como separador de dígitos.
- C# 7.2 permite usar `_` como separador de dígitos de un literal binario o hexadecimal, después del prefijo. Un literal decimal no puede tener un carácter de subrayado inicial.

A continuación se muestran algunos ejemplos.

[!code-csharp[SByteSeparator](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#SByteS)]

Si el literal entero está fuera del intervalo de `sbyte` (es decir, si es inferior a <xref:System.SByte.MinValue?displayProperty=nameWithType> o mayor que <xref:System.SByte.MaxValue?displayProperty=nameWithType>, se produce un error de compilación. Cuando un literal entero no tiene sufijo, su tipo es el primero de estos tipos en el que se puede representar su valor: [int](int.md), [uint](uint.md), [long](long.md), [ulong](ulong.md). Esto significa que, en este ejemplo, los literales numéricos `0x9A` y `0b10011010` se interpretan como enteros con signo de 32 bits con un valor de 156, que supera <xref:System.SByte.MaxValue?displayProperty=nameWithType>. Por este motivo, se necesita el operador de conversión, y debe producirse la asignación en un contexto [desactivado](unchecked.md).

## <a name="compiler-overload-resolution"></a>Resolución de sobrecarga del compilador

Debe usarse una conversión de tipos al llamar a métodos sobrecargados. Por ejemplo, considere los siguientes métodos sobrecargados que usan parámetros `sbyte` e [int](../../../csharp/language-reference/keywords/int.md):

```csharp
public static void SampleMethod(int i) {}
public static void SampleMethod(sbyte b) {}
```

El uso de la conversión `sbyte` garantiza que se llama al tipo correcto, por ejemplo:

```csharp
// Calling the method with the int parameter:
SampleMethod(5);
// Calling the method with the sbyte parameter:
SampleMethod((sbyte)5);
```

## <a name="conversions"></a>Conversiones

Existe una conversión implícita predefinida de `sbyte` a [short](../../../csharp/language-reference/keywords/short.md), [int](../../../csharp/language-reference/keywords/int.md), [long](../../../csharp/language-reference/keywords/long.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) o [decimal](../../../csharp/language-reference/keywords/decimal.md).

No se pueden convertir implícitamente los tipos numéricos no literales de mayor tamaño de almacenamiento a `sbyte` (vea en la [Tabla de tipos enteros](../../../csharp/language-reference/keywords/integral-types-table.md) los tamaños de almacenamiento de los tipos enteros). Considere, por ejemplo, las dos siguientes variables de `sbyte` `x` e `y`:

```csharp
sbyte x = 10, y = 20;
```

La instrucción de asignación siguiente producirá un error de compilación porque la expresión aritmética del lado derecho del operador de asignación da como resultado [int](../../../csharp/language-reference/keywords/int.md) de forma predeterminada.

```csharp
sbyte z = x + y;   // Error: conversion from int to sbyte
```

Para corregir este problema, convierta la expresión como en el ejemplo siguiente:

```csharp
sbyte z = (sbyte)(x + y);   // OK: explicit conversion
```

Pero es posible usar las instrucciones siguientes cuando la variable de destino tiene el mismo tamaño de almacenamiento o un tamaño de almacenamiento mayor:

```csharp
sbyte x = 10, y = 20;
int m = x + y;
long n = x + y;
```

Observe también que no hay ninguna conversión implícita de tipos de punto flotante a `sbyte`. Por ejemplo, la instrucción siguiente genera un error del compilador, a menos que se use una conversión explícita:

```csharp
sbyte x = 3.0;         // Error: no implicit conversion from double
sbyte y = (sbyte)3.0;  // OK: explicit conversion
```

Para obtener información sobre expresiones aritméticas con combinaciones de tipos de punto flotante y tipos enteros, vea [float](../../../csharp/language-reference/keywords/float.md) y [double](../../../csharp/language-reference/keywords/double.md).

Para obtener más información sobre las reglas de conversión numéricas implícitas, vea la [Tabla de conversiones numéricas implícitas](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).

## <a name="c-language-specification"></a>Especificación del lenguaje C#

Para obtener más información, vea la sección [Tipos enteros](~/_csharplang/spec/types.md#integral-types) de la [Especificación del lenguaje C#](../language-specification/index.md). La especificación del lenguaje es la fuente definitiva de la sintaxis y el uso de C#.

## <a name="see-also"></a>Vea también

- <xref:System.SByte>
- [Referencia de C#](../../../csharp/language-reference/index.md)
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Palabras clave de C#](../../../csharp/language-reference/keywords/index.md)
- [Tabla de tipos enteros](../../../csharp/language-reference/keywords/integral-types-table.md)
- [Tabla de tipos integrados](../../../csharp/language-reference/keywords/built-in-types-table.md)
- [Tabla de conversiones numéricas implícitas](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)
- [Tabla de conversiones numéricas explícitas](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
