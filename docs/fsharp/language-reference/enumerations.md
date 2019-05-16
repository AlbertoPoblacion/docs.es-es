---
title: Enumeraciones
description: Aprenda a usar F# enumeraciones en lugar de literales para que el código más legible y fácil de mantener.
ms.date: 05/16/2016
ms.openlocfilehash: 7ff62b1c0a6ab0fda58a30de9387acbb547f6b81
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645553"
---
# <a name="enumerations"></a>Enumeraciones

*Enumeraciones*, también conocida como *enumeraciones*,, son tipos enteros donde las etiquetas se asignan a un subconjunto de los valores. Se pueden usar en lugar de los literales para que el código sea más fácil de leer y mantener.

## <a name="syntax"></a>Sintaxis

```fsharp
type enum-name =
| value1 = integer-literal1
| value2 = integer-literal2
...
```

## <a name="remarks"></a>Comentarios

Una enumeración se parece mucho a una unión discriminada que tiene valores simples, salvo que se pueden especificar los valores. Normalmente, los valores son enteros que comienzan en 0 o 1 o enteros que representan las posiciones de bits. Si una enumeración está pensada para representar las posiciones de bits, también se debe utilizar el [marcas](xref:System.FlagsAttribute) atributo.

El tipo subyacente de la enumeración se determina a partir del literal que se usa, por lo que, por ejemplo, puede usar literales con sufijo, como `1u`, `2u`, y así sucesivamente, para un entero sin signo (`uint32`) tipo.

Cuando se hace referencia a los valores con nombre, debe usar el nombre del propio tipo de enumeración como un calificador, es decir, `enum-name.value1`, no sólo `value1`. Este comportamiento difiere de las uniones discriminadas. Esto es porque las enumeraciones siempre tienen la [RequireQualifiedAccess](https://msdn.microsoft.com/library/8b9b6ade-0471-4413-ac5d-638cd0de5f15) atributo.

El código siguiente muestra la declaración y el uso de una enumeración.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2101.fs)]

Puede convertir fácilmente las enumeraciones con el tipo subyacente mediante el operador adecuado, tal como se muestra en el código siguiente.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2102.fs)]

Los tipos enumerados pueden tener uno de los siguientes tipos subyacentes: `sbyte`, `byte`, `int16`, `uint16`, `int32`, `uint32`, `int64`, `uint16`, `uint64`, y `char`. Tipos de enumeración se representan en .NET Framework como tipos que se heredan de `System.Enum`, que a su vez se hereda de `System.ValueType`. Por lo tanto, son tipos de valor que se encuentran en la pila o en línea en el objeto contenedor, y cualquier valor del tipo subyacente es un valor válido de la enumeración. Esto es importante cuando los valores de coincidencia de patrones en la enumeración, ya que hay que proporcionar un patrón que detecta los valores sin nombre.

El `enum` funcionando en el F# biblioteca puede utilizarse para generar un valor de enumeración, incluso un valor distinto de uno de los predefinidos, valores con nombre. Usa el `enum` funcione como se indica a continuación.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2103.fs)]

El valor predeterminado `enum` función funciona con el tipo `int32`. Por lo tanto, no se puede usar con tipos de enumeración que tienen otros tipos subyacentes. En su lugar, use lo siguiente.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2104.fs)]

Además, los casos, para las enumeraciones siempre se emiten como `public`. Esto es para que se alineen con C# y el resto de la plataforma. NET.

## <a name="see-also"></a>Vea también

- [Referencia del lenguaje F#](index.md)
- [Conversiones](casting-and-conversions.md)
