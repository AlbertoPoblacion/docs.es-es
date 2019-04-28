---
title: CType (Función) (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.CType
helpviewer_keywords:
- expression conversion results
- explicit data type conversions [Visual Basic]
- CType function
- conversions [Visual Basic], expression
ms.assetid: dd4b29e7-6fa1-428c-877e-69955420bb72
ms.openlocfilehash: dbf01263723a9e2890dab57d5ffc3d467ed250fc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61801684"
---
# <a name="ctype-function-visual-basic"></a>CType (Función) (Visual Basic)

Devuelve el resultado de convertir explícitamente una expresión en una estructura, clase, tipo de datos especificado, objeto o interfaz.

## <a name="syntax"></a>Sintaxis

```
CType(expression, typename)
```

## <a name="parts"></a>Elementos

`expression` Cualquier expresión válida. Si el valor de `expression` está fuera del intervalo permitido por `typename`, Visual Basic produce una excepción.

`typename` Cualquier expresión válida dentro de un `As` cláusula en una `Dim` instrucción, es decir, el nombre de cualquier tipo de datos objeto, estructura, clase o interfaz.

## <a name="remarks"></a>Comentarios

> [!TIP]
> También puede usar las siguientes funciones para realizar una conversión de tipos:
>
> - Funciones de conversión de tipos como `CByte`, `CDbl`, y `CInt` que realizar una conversión a un tipo de datos específico. Para obtener más información, consulte [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md).
> - [DirectCast (operador)](../../../visual-basic/language-reference/operators/directcast-operator.md) o [TryCast (operador)](../../../visual-basic/language-reference/operators/trycast-operator.md). Estos operadores requieren que un tipo herede o implemente en otro tipo. Puede proporcionar un mejor rendimiento que `CType` al convertir desde y hacia el `Object` tipo de datos.

`CType` está compilado en línea, lo que significa que el código de conversión forma parte del código que evalúa la expresión. En algunos casos, el código se ejecuta con mayor rapidez porque no se llama a ningún procedimiento para llevar a cabo la conversión.

Si no se ha definido ninguna conversión de `expression` a `typename` (por ejemplo, desde `Integer` a `Date`), Visual Basic muestra un mensaje de error de tiempo de compilación.

Si se produce un error en una conversión en tiempo de ejecución, se produce la excepción adecuada. Si se produce un error en una conversión de restricción, una <xref:System.OverflowException> es el resultado más común. Si la conversión es indefinida, un <xref:System.InvalidCastException> en produce. Por ejemplo, esto puede suceder si `expression` es de tipo `Object` y su tipo en tiempo de ejecución no tiene ninguna conversión a `typename`.

Si el tipo de datos de `expression` o `typename` es una clase o estructura que ha definido, puede definir `CType` en esa clase o estructura como un operador de conversión. Esto hace que `CType` actuar como un *operador sobrecargado*. Si lo hace, puede controlar el comportamiento de las conversiones a y desde la clase o estructura, incluidas las excepciones que se pueden producir.

## <a name="overloading"></a>Sobrecarga

El `CType` también se puede sobrecargar el operador en una clase o estructura definida fuera del código. Si el código realiza conversiones a o desde una clase o estructura de este tipo, asegúrese de comprender el comportamiento de su `CType` operador. Para obtener más información, consulta [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).

## <a name="converting-dynamic-objects"></a>Convertir objetos dinámicos

Las conversiones de tipos de objetos dinámicos se realizan mediante conversiones dinámicas definidas por el usuario que utilizan el <xref:System.Dynamic.DynamicObject.TryConvert%2A> o <xref:System.Dynamic.DynamicMetaObject.BindConvert%2A> métodos. Si está trabajando con objetos dinámicos, utilice el <xref:Microsoft.VisualBasic.Conversion.CTypeDynamic%2A> método para convertir el objeto dinámico.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se usa el `CType` función para convertir una expresión a la `Single` tipo de datos.

[!code-vb[VbVbalrFunctions#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrFunctions/VB/Class1.vb#24)]

Para obtener ejemplos adicionales, consulte [conversiones implícitas y explícitas](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md).

## <a name="see-also"></a>Vea también

- <xref:System.OverflowException>
- <xref:System.InvalidCastException>
- [Funciones de conversión de tipos](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [Funciones de conversión](../../../visual-basic/language-reference/functions/conversion-functions.md)
- [Operator (instrucción)](../../../visual-basic/language-reference/statements/operator-statement.md)
- [Cómo: Definir un operador de conversión](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)
- [Conversión de tipos en .NET Framework](../../../standard/base-types/type-conversion.md)
