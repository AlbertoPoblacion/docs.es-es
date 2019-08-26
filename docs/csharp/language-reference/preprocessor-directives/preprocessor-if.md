---
title: '#Directiva de preprocesador if: Referencia de C#'
ms.custom: seodec18
ms.date: 06/30/2018
f1_keywords:
- '#if'
helpviewer_keywords:
- '#if directive [C#]'
ms.assetid: 48cabbff-ca82-491f-a56a-eeccd528c7c2
ms.openlocfilehash: d0297094fbb8098b706cb8c6338fa123afc0753b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2019
ms.locfileid: "69605687"
---
# <a name="if-c-reference"></a>#if (Referencia de C#)

Cuando el compilador de C# encuentra una directiva `#if`, seguida finalmente por una directiva [#endif](preprocessor-endif.md), compila el código entre las directivas solo si se ha definido el símbolo especificado. A diferencia de C y C++, no se puede asignar un valor numérico a un símbolo. La instrucción #if en C# es booleana y solo comprueba si el símbolo se ha definido o no. Por ejemplo:

```csharp
#if DEBUG
    Console.WriteLine("Debug version");
#endif
```

Puede usar los operadores [==](../operators/equality-operators.md#equality-operator-) (igualdad) y [!=](../operators/equality-operators.md#inequality-operator-) (desigualdad) solo para comprobar los valores [true](../keywords/true-literal.md) o [false](../keywords/false-literal.md). True significa que el símbolo está definido. La instrucción `#if DEBUG` tiene el mismo significado que `#if (DEBUG == true)`. Puede usar los operadores [&&](../operators/boolean-logical-operators.md#conditional-logical-and-operator-) (y), [&#124;&#124;](../operators/boolean-logical-operators.md#conditional-logical-or-operator-) (o) y [!](../operators/boolean-logical-operators.md#logical-negation-operator-) (no) para evaluar si se han definido varios símbolos. Es posible agrupar símbolos y operadores mediante paréntesis.

## <a name="remarks"></a>Comentarios

`#if`, junto con las directivas [#else](preprocessor-else.md), [#elif](preprocessor-elif.md), [#endif](preprocessor-endif.md), [#define](preprocessor-define.md) y [#undef](preprocessor-undef.md), permite incluir o excluir código basado en la existencia de uno o varios símbolos. Esto puede resultar útil al compilar código para una compilación de depuración o al compilar para una configuración específica.

Una directiva condicional que empieza con una directiva `#if` debe terminar de forma explícita con una directiva `#endif`.

`#define` permite definir un símbolo. Si luego se usa el símbolo como la expresión pasada a la directiva `#if`, la expresión se evalúa como `true`.

También se puede definir un símbolo con la opción del compilador [-define](../compiler-options/define-compiler-option.md). La definición de un símbolo se puede anular mediante [#undef](preprocessor-undef.md).

Un símbolo definido con `-define` o `#define` no debe entrar en conflicto con una variable del mismo nombre. Es decir, un nombre de variable no debe pasarse a una directiva de preprocesador y un símbolo solo puede ser evaluado por una directiva de preprocesador.

El ámbito de un símbolo creado con `#define` es el archivo en que se ha definido.

El sistema de compilación también tiene en cuenta los símbolos de preprocesador predefinidos que representan distintos [marcos de destino](../../../standard/frameworks.md). Resultan útiles al crear aplicaciones que pueden tener como destino más de una versión o implementación de .NET.

[!INCLUDE [Preprocessor symbols](~/includes/preprocessor-symbols.md)]

Otros símbolos predefinidos incluyen las constantes DEBUG y TRACE. Puede invalidar los valores establecidos para el proyecto con `#define`. Por ejemplo, el símbolo DEBUG se establece automáticamente según las propiedades de configuración de compilación (modo de "depuración" o de "versión").

## <a name="examples"></a>Ejemplos

En el ejemplo siguiente se muestra cómo definir un símbolo MYTEST en un archivo y luego probar los valores de los símbolos MYTEST y DEBUG. El resultado de este ejemplo depende de si ha compilado el proyecto en modo de configuración de depuración o de versión.

```csharp
#define MYTEST
using System;
public class MyClass
{
    static void Main()
    {
#if (DEBUG && !MYTEST)
        Console.WriteLine("DEBUG is defined");
#elif (!DEBUG && MYTEST)
        Console.WriteLine("MYTEST is defined");
#elif (DEBUG && MYTEST)
        Console.WriteLine("DEBUG and MYTEST are defined");  
#else
        Console.WriteLine("DEBUG and MYTEST are not defined");
#endif
    }
}
```

En el ejemplo siguiente se muestra cómo probar distintos marcos de destino para que se puedan usar las API más recientes cuando sea posible:

```csharp
public class MyClass
{
    static void Main()
    {
#if NET40
        WebClient _client = new WebClient();
#else
        HttpClient _client = new HttpClient();
#endif
    }
    //...
}
```

## <a name="see-also"></a>Vea también

- [Referencia de C#](../index.md)
- [Guía de programación de C#](../../programming-guide/index.md)
- [Directivas de preprocesador de C#](index.md)
- [Cómo: Compilación condicional con Trace y Debug](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)
