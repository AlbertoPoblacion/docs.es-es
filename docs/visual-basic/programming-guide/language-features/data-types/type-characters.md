---
title: Caracteres de tipo (Visual Basic)
ms.date: 01/31/2018
helpviewer_keywords:
- '&H prefix for hexadecimal values'
- hexadecimal literals [Visual Basic]
- F literal type character [Visual Basic]
- '& identifier type character'
- type characters [Visual Basic]
- octal literals [Visual Basic]
- literals [Visual Basic], hexadecimal
- '&O prefix for octal values'
- literals [Visual Basic], default types
- defaults, literal types
- C literal type character [Visual Basic]
- type characters [Visual Basic], literal
- $ identifier type character
- L literal type character [Visual Basic]
- UI literal type characters [Visual Basic]
- default literal types [Visual Basic]
- D literal type character [Visual Basic]
- literals [Visual Basic], octal
- S literal type character [Visual Basic]
- '! identifier type character'
- US literal type characters [Visual Basic]
- '% identifier type character'
- data types [Visual Basic], type characters
- characters [Visual Basic], identifier type
- type characters [Visual Basic], identifier
- '# identifier type character'
- identifier type characters [Visual Basic]
- literal type characters [Visual Basic]
- I literal type character [Visual Basic]
- R literal type character [Visual Basic]
- '@ identifier type character'
- UL literal type characters [Visual Basic]
- literal types [Visual Basic], default
ms.assetid: 6353cb9b-6ee4-4af6-a5a8-88ce39f90cc5
ms.openlocfilehash: a469a08ebadd77d5abbfa95b270784c9ef534691
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61906755"
---
# <a name="type-characters-visual-basic"></a>Escriba caracteres (Visual Basic)

Además de especificar un tipo de datos en una instrucción de declaración, puede forzar el tipo de datos de algunos elementos de programación con un *carácter de tipo*. El carácter de tipo debe aparecer inmediatamente después del elemento, sin caracteres intermedios de ningún tipo.

El carácter de tipo no es parte del nombre del elemento. Puede hacer referencia a un elemento definido con un carácter de tipo sin el carácter de tipo.

## <a name="identifier-type-characters"></a>Caracteres de tipo identificador

Visual Basic proporciona un conjunto de *caracteres de tipo identificador* que puede usar en una declaración para especificar el tipo de datos de una variable o constante. En la tabla siguiente se muestra los caracteres de tipo identificador disponibles con ejemplos de uso.
  
|Carácter de tipo identificador|Tipo de datos|Ejemplo|  
|-------------------------------|---------------|-------------|  
|`%`|`Integer`|`Dim L%`|  
|`&`|`Long`|`Dim M&`|  
|`@`|`Decimal`|`Const W@ = 37.5`|  
|`!`|`Single`|`Dim Q!`|  
|`#`|`Double`|`Dim X#`|  
|`$`|`String`|`Dim V$ = "Secret"`|  
  
 No existe ningún carácter de tipo identificador para el `Boolean`, `Byte`, `Char`, `Date`, `Object`, `SByte`, `Short`, `UInteger`, `ULong`, o `UShort` tipos de datos, o para ninguno tipos de datos compuestos como matrices o estructuras.

En algunos casos, puede anexar el `$` de caracteres a una función de Visual Basic, por ejemplo `Left$` en lugar de `Left`, para obtener un valor devuelto de tipo `String`.

En todos los casos, el carácter de tipo identificador debe aparecer inmediatamente después del nombre del identificador.

## <a name="literal-type-characters"></a>Caracteres de tipo literal

Un *literal* es una representación textual de un valor determinado de un tipo de datos.  

### <a name="default-literal-types"></a>Tipos literales predeterminados

El formato de un literal tal como aparece en el código normalmente determina su tipo de datos. En la tabla siguiente se muestra estos tipos de forma predeterminada.  
  
|Formato textual de literal|Tipo de datos predeterminado|Ejemplo|  
|-----------------------------|-----------------------|-------------|  
|Numérico, ninguna parte fraccionaria|`Integer`|`2147483647`|  
|Numérico, ninguna parte fraccionaria, demasiado grande para `Integer`|`Long`|`2147483648`|  
|Numérico, parte fraccionaria|`Double`|`1.2`|  
|Entre comillas dobles|`String`|`"A"`|  
|Encerrado entre signos de número|`Date`|`#5/17/1993 9:32 AM#`|  

### <a name="forced-literal-types"></a>Tipos literales forzados

Visual Basic proporciona un conjunto de *caracteres de tipo literal*, lo que puede usar para forzar un literal se supone un tipo de datos que no sea el de su formulario indica. Para ello, anexe el carácter al final del literal. La siguiente tabla muestra los caracteres de tipo literal disponibles con ejemplos de uso.
  
|Carácter de tipo literal|Tipo de datos|Ejemplo|  
|----------------------------|---------------|-------------|  
|`S`|`Short`|`I = 347S`|
|`I`|`Integer`|`J = 347I`|
|`L`|`Long`|`K = 347L`|
|`D`|`Decimal`|`X = 347D`|
|`F`|`Single`|`Y = 347F`|
|`R`|`Double`|`Z = 347R`|
|`US`|`UShort`|`L = 347US`|
|`UI`|`UInteger`|`M = 347UI`|
|`UL`|`ULong`|`N = 347UL`|
|`C`|`Char`|`Q = "."C`|

No existe ningún carácter de tipo literal para el `Boolean`, `Byte`, `Date`, `Object`, `SByte`, o `String` tipos de datos, o para los tipos de datos compuestos como matrices o estructuras.

Los literales también pueden utilizar los caracteres de tipo identificador (`%`, `&`, `@`, `!`, `#`, `$`), igual que las variables, constantes y expresiones. Sin embargo, el literal de tipo caracteres (`S`, `I`, `L`, `D`, `F`, `R`, `C`) puede utilizarse solo con literales.

En todos los casos, el carácter de tipo literal debe seguir inmediatamente el valor literal.

## <a name="hexadecimal-binary-and-octal-literals"></a>Literales hexadecimales, binarios y octales

Normalmente, el compilador interpreta un literal entero para estar en el sistema numérico decimal (base 10). También puede definir un literal entero como un número hexadecimal (base 16) con el `&H` prefijo, como un número binario (base 2) con el `&B` prefijo y como un octal (base 8) con el `&O` prefijo. Los dígitos que siguen el prefijo deben ser adecuados para el sistema numérico. En la tabla siguiente se ilustra esto.  
  
|Número base|Prefijo|Valores de dígito válido|Ejemplo|
|-----------------|------------|------------------------|-------------|
|Hexadecimal (base 16)|`&H`|0-9 y A-F|`&HFFFF`|
|Binario (base 2)|`&B`|0-1|`&B01111100`|
|Octal (base 8)|`&O`|0-7|`&O77`|

A partir de Visual Basic 2017, puede usar el carácter de subrayado (`_`) como un separador de grupo para mejorar la legibilidad de un literal entero. En el ejemplo siguiente se usa el `_` caracteres para agrupar un literal binario en grupos de 8 bits:

```vb
Dim number As Integer = &B00100010_11000101_11001111_11001101
```

Puede agregar un literal prefijado con un carácter de tipo literal. En el ejemplo siguiente se muestra esto.

```vb
Dim counter As Short = &H8000S
Dim flags As UShort = &H8000US
```

En el ejemplo anterior, `counter` tiene el valor decimal entre-32768, y `flags` tiene el valor decimal de + 32768.

A partir de Visual Basic 15.5, también puede usar el carácter de subrayado (`_`) como separador inicial entre el prefijo y los dígitos hexadecimales, binarios u octales. Por ejemplo:

```vb
Dim number As Integer = &H_C305_F860
```

[!INCLUDE [supporting-underscores](../../../../../includes/vb-separator-langversion.md)]

## <a name="see-also"></a>Vea también

- [Tipos de datos](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
- [Tipos de datos básicos](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)
- [Value Types and Reference Types](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
- [Conversiones de tipos en Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)
- [Solución de problemas de tipos de datos](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [Declaración de variables](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)
- [Tipos de datos](../../../../visual-basic/language-reference/data-types/index.md)
