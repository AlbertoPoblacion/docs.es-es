---
title: 'Excepciones: Expresión try...finally'
description: Obtenga información sobre cómo el F# ' try... finally' expresión permite ejecutar código de limpieza, incluso si un bloque de código produce una excepción.
ms.date: 05/16/2016
ms.openlocfilehash: d246bce52b5f30d5e8d7e3c36e9f7d7c48627913
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645463"
---
# <a name="exceptions-the-tryfinally-expression"></a>Excepciones: Expresión try...finally

El `try...finally` expresión permite ejecutar código de limpieza, incluso si un bloque de código produce una excepción.

## <a name="syntax"></a>Sintaxis

```fsharp
try
    expression1
finally
    expression2
```

## <a name="remarks"></a>Comentarios

El `try...finally` expresión puede utilizarse para ejecutar el código en *expression2* en la sintaxis anterior, independientemente de si se genera una excepción durante la ejecución de *expression1*.

El tipo de *expression2* no contribuyen al valor de la expresión completa; el tipo devuelto cuando no se produce una excepción es el último valor en *expression1*. Cuando se produce una excepción, se devuelve ningún valor y el flujo de control se transfiere al siguiente controlador de excepción coincidente en la pila de llamadas. Si no se encuentra ningún controlador de excepción, el programa finaliza. Antes de que se ejecuta el código en un controlador coincidente o el programa finaliza, el código en el `finally` se ejecuta la rama.

El código siguiente muestra el uso de la `try...finally` expresión.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5701.fs)]

El resultado de la consola es como sigue.

```
Closing stream
Exception handled.
```

Como puede ver en la salida, la secuencia se cerró antes de que se ha controlado la excepción externa y el archivo `test.txt` contiene el texto `test1`, que indica que los búferes se vacían y escritos en el disco, aunque se transfiere de la excepción control al controlador de excepción externa.

Tenga en cuenta que el `try...with` construcción es una construcción independiente de la `try...finally` construir. Por lo tanto, si el código requiere tanto un `with` bloque y un `finally` bloque, tendrá que anidar las dos construcciones, como se muestra en el siguiente ejemplo de código.

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-2/snippet5702.fs)]

En el contexto de las expresiones de cálculo, incluidas las expresiones de secuencia y flujos de trabajo asincrónicos, **try... finally** las expresiones pueden tener una implementación personalizada. Para obtener más información, consulte [expresiones de cálculo](../computation-expressions.md).

## <a name="see-also"></a>Vea también

- [Control de excepciones](index.md)
- [Excepciones: El `try...with` expresión](the-try-with-expression.md)
