---
title: Instrucción For Each...Next (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.ForEach
- vb.ForEachNext
- vb.Each
- ForEachNext
helpviewer_keywords:
- infinite loops
- Next statement [Visual Basic], For Each...Next
- endless loops
- loop structures [Visual Basic], For Each...Next
- loops, endless
- Each keyword [Visual Basic]
- instructions, repeating
- For Each statement [Visual Basic]
- collections, instruction repetition
- loops, infinite
- For Each...Next statements
- For keyword [Visual Basic], For Each...Next statements
- Exit statement [Visual Basic], For Each...Next statements
- iteration
ms.assetid: ebce3120-95c3-42b1-b70b-fa7da40c75e2
ms.openlocfilehash: 5081f80ad0da738ebb950bcd649af7a593582356
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58824354"
---
# <a name="for-eachnext-statement-visual-basic"></a>Instrucción For Each...Next (Visual Basic)
Repite un grupo de instrucciones para cada elemento de una colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
For Each element [ As datatype ] In group  
    [ statements ]  
    [ Continue For ]  
    [ statements ]  
    [ Exit For ]  
    [ statements ]  
Next [ element ]  
```  
  
## <a name="parts"></a>Elementos  
  
|Término|Definición|  
|---|---|  
|`element`|Necesario en el `For Each` instrucción. Opcional en el `Next` instrucción. Variable. Se utiliza para recorrer en iteración los elementos de la colección.|  
|`datatype`|Es necesario si `element` ya no está declarado. Tipo de datos de `element`.|  
|`group`|Obligatorio. Una variable con un tipo que es un tipo de colección o el objeto. Hace referencia a la colección en el que el `statements` a repetirse.|  
|`statements`|Opcional. Una o varias instrucciones entre `For Each` y `Next` que se ejecutan en cada elemento de `group`.|  
|`Continue For`|Opcional. Transfiere el control al principio de la `For Each` bucle.|  
|`Exit For`|Opcional. Transfiere el control fuera de la `For Each` bucle.|  
|`Next`|Obligatorio. Termina la definición de la `For Each` bucle.|  
  
## <a name="simple-example"></a>Ejemplo sencillo  
 Use un `For Each`... `Next` bucle cuando desea repetir un conjunto de instrucciones para cada elemento de una colección o matriz.  
  
> [!TIP]
>  Un [para... Instrucción Next](../../../visual-basic/language-reference/statements/for-next-statement.md) funciona bien cuando puede asociar cada iteración de un bucle a una variable de control y determinar los valores inicial y final de la variable. Sin embargo, cuando se trata de una colección, el concepto de valores iniciales y finales no es significativo y no necesariamente saber cuántos elementos tiene la colección. En este tipo de caso, un `For Each`... `Next` bucle suele ser una opción mejor.  
  
 En el ejemplo siguiente, la `For Each`...`Next` instrucción recorre en iteración todos los elementos de una colección de lista.  
  
 [!code-vb[VbVbalrStatements#121](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#121)]  
  
 Para obtener más ejemplos, vea [colecciones](../../../standard/collections/index.md) y [matrices](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
## <a name="nested-loops"></a>Bucles anidados  
 Puede anidar `For Each` bucles colocando un bucle dentro de otro.  
  
 En el ejemplo siguiente se muestra anidada `For Each`...`Next` estructuras.  
  
 [!code-vb[VbVbalrStatements#122](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#122)]  
  
 Al anidar bucles, cada bucle debe tener un único `element` variable.  
  
 También puede anidar diferentes tipos de estructuras de control entre sí. Para obtener más información, consulte [estructuras de Control anidadas](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
## <a name="exit-for-and-continue-for"></a>Salir de y continuar para  
 El [Exit For](../../../visual-basic/language-reference/statements/exit-statement.md) instrucción provoca la ejecución al salir el `For`...`Next` bucle y transfiere el control a la instrucción que sigue la `Next` instrucción.  
  
 El `Continue For` instrucción transfiere el control inmediatamente a la siguiente iteración del bucle. Para obtener más información, consulte [instrucción Continue](../../../visual-basic/language-reference/statements/continue-statement.md).  
  
 El ejemplo siguiente muestra cómo usar el `Continue For` y `Exit For` instrucciones.  
  
 [!code-vb[VbVbalrStatements#123](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#123)]  
  
 Puede colocar cualquier número de `Exit For` instrucciones en un `For Each` bucle. Cuando se usa dentro de anidar `For Each` bucles, `Exit For` provoca la ejecución al salir del bucle y transfiere el control más interno al siguiente nivel más alto de anidamiento.  
  
 `Exit For` a menudo se usa después de una evaluación de alguna condición, por ejemplo, en un `If`... `Then`... `Else` estructura. Desea usar `Exit For` para las condiciones siguientes:  
  
-   Continuar recorrer en iteración es innecesarios o imposible. Esto podría deberse a un valor erróneo o una solicitud de finalización.  
  
-   Se detectó una excepción en un `Try`... `Catch`... `Finally`. Puede usar `Exit For` al final de la `Finally` bloque.  
  
-   Hay un bucle sin fin, que es un bucle que podría ejecutar un número grande o incluso infinito de veces. Si se detecta una condición de ese tipo, puede usar `Exit For` para salir del bucle. Para obtener más información, consulte [hacer... Instrucción de bucle](../../../visual-basic/language-reference/statements/do-loop-statement.md).  
  
## <a name="iterators"></a>Iterators  
 Usa un *iterador* para realizar una iteración personalizada en una colección. Un iterador puede ser una función o un `Get` descriptor de acceso. Usa un `Yield` instrucción para devolver cada elemento de la colección a la vez.  
  
 Llame a un iterador mediante una `For Each...Next` instrucción. Cada iteración del bucle `For Each` llama al iterador. Cuando un `Yield` se alcanza la instrucción en el iterador, la expresión en el `Yield` instrucción se devuelve y se conserva la ubicación actual en el código. La ejecución se reinicia desde esa ubicación la próxima vez que se llama al iterador.  
  
 El ejemplo siguiente usa una función de iterador. La función de iterador tiene una `Yield` instrucción que está dentro de un [para... Siguiente](../../../visual-basic/language-reference/statements/for-next-statement.md) bucle. En el `ListEvenNumbers` método, cada iteración de la `For Each` cuerpo de la instrucción crea una llamada a la función de iterador, que continúa con la siguiente `Yield` instrucción.  
  
 [!code-vb[VbVbalrStatements#127](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#127)]  
  
 Para obtener más información, consulte [iteradores](../../programming-guide/concepts/iterators.md), [instrucción Yield](../../../visual-basic/language-reference/statements/yield-statement.md), y [iterador](../../../visual-basic/language-reference/modifiers/iterator.md).  
  
## <a name="technical-implementation"></a>Implementación técnica  
 Cuando un `For Each`...`Next` instrucción se ejecuta, Visual Basic se evalúa como la colección de solo una vez, antes de que comience el bucle. Si cambia el bloque de instrucciones `element` o `group`, estos cambios no afectan a la iteración del bucle.  
  
 Cuando todos los elementos de la colección se ha asignado correctamente a `element`, `For Each` bucle se detiene y el control pasa a la instrucción que sigue la `Next` instrucción.  
  
 Si `element` aún no se ha declarado fuera de este bucle, se debe declarar en el `For Each` instrucción. Se puede declarar el tipo de `element` explícitamente mediante una `As` instrucción, o bien puede basarse en la inferencia de tipos para asignar el tipo. En cualquier caso, el ámbito de `element` es el cuerpo del bucle. Sin embargo, no puede declarar `element` fuera y dentro del bucle.  
  
 Opcionalmente, puede especificar `element` en el `Next` instrucción. Esto mejora la legibilidad del programa, especialmente si ha anidado `For Each` bucles. Debe especificar la misma variable que aparecerá en las correspondientes `For Each` instrucción.  
  
 Desea evitar cambiar el valor de `element` dentro de un bucle. Esto puede hacer más difícil de leer y depurar el código. Cambiar el valor de `group` no afecta a la colección o sus elementos, que se han determinado cuando el bucle se introdujo en primer lugar.  
  
 Cuando está anidar bucles, si un `Next` instrucción de un nivel de anidamiento externo se encuentra antes del `Next` de un nivel interno, el compilador señala un error. Sin embargo, el compilador puede detectar esta superposición de error únicamente si se especifica `element` en cada `Next` instrucción.  
  
 Si el código depende de recorrido de una colección en un orden determinado, un `For Each`... `Next` bucle no es la mejor opción, a menos que conozca las características del objeto enumerador que expone la colección. No se determina el orden del recorrido por Visual Basic, sino por la <xref:System.Collections.IEnumerator.MoveNext%2A> método del objeto enumerador. Por lo tanto, es posible que no pueda predecir qué elemento de la colección es el primero que se devolverán en `element`, o que es el siguiente que se devuelve después de un elemento determinado. Puede conseguir resultados más confiables con una estructura de bucle diferente, como `For`... `Next` o `Do`... `Loop`.  
  
 Tipo de datos de `element` será tal que el tipo de datos de los elementos de `group` se pueden convertir a él.  
  
 Tipo de datos de `group` debe ser un tipo de referencia que hace referencia a una colección o una matriz que es enumerable. Normalmente, esto significa que `group` hace referencia a un objeto que implementa el <xref:System.Collections.IEnumerable> interfaz de la `System.Collections` espacio de nombres o el <xref:System.Collections.Generic.IEnumerable%601> interfaz de la `System.Collections.Generic` espacio de nombres. `System.Collections.IEnumerable` define el <xref:System.Collections.IEnumerable.GetEnumerator%2A> método, que devuelve un objeto enumerador para la colección. El objeto de enumerador implementa el `System.Collections.IEnumerator` interfaz de la `System.Collections` espacio de nombres y expone el <xref:System.Collections.IEnumerator.Current%2A> propiedad y el <xref:System.Collections.IEnumerator.Reset%2A> y <xref:System.Collections.IEnumerator.MoveNext%2A> métodos. Visual Basic utiliza estos para recorrer la colección.  
  
### <a name="narrowing-conversions"></a>conversiones de restricción  
 Cuando `Option Strict` está establecido en `On`, las conversiones de restricción suelen provocan errores del compilador. En un `For Each` instrucción, sin embargo, las conversiones de los elementos de `group` a `element` se evalúan y se realiza en tiempo de ejecución y se suprimen los errores del compilador causados por las conversiones de restricción.  
  
 En el ejemplo siguiente, la asignación de `m` como valor inicial para `n` no se compila cuando `Option Strict` está activado porque la conversión de un `Long` a un `Integer` es una conversión de restricción. En el `For Each` instrucción, sin embargo, ningún error del compilador es notificado, aunque la asignación a `number` requiere la misma conversión desde `Long` a `Integer`. En el `For Each` instrucción que contiene un número grande, que se produce un error en tiempo de ejecución cuando <xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A> se aplica a la gran cantidad.  
  
 [!code-vb[VbVbalrStatements#89](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class3.vb#89)]  
  
### <a name="ienumerator-calls"></a>Llamadas de IEnumerator  
 Cuando la ejecución de un `For Each`... `Next` bucle inicia, Visual Basic comprueba que `group` hace referencia a un objeto de colección válido. Si no es así, produce una excepción. De lo contrario, llama el <xref:System.Collections.IEnumerator.MoveNext%2A> método y el <xref:System.Collections.IEnumerator.Current%2A> propiedad del objeto enumerador para devolver el primer elemento. Si `MoveNext` no indica que no existe ningún elemento siguiente, es decir, si la colección está vacía, el `For Each` bucle se detiene y el control pasa a la instrucción que sigue la `Next` instrucción. En caso contrario, Visual Basic establece `element` para el primer elemento y se ejecuta el bloque de instrucciones.  
  
 Cada vez que Visual Basic encuentra la `Next` instrucción, devuelve a la `For Each` instrucción. Llama de nuevo `MoveNext` y `Current` para devolver el elemento siguiente y, nuevamente uno ejecuta el bloque o detiene el bucle según el resultado. Este proceso continúa hasta que `MoveNext` indica que no hay ningún elemento siguiente o `Exit For` se encuentra la instrucción.  
  
 **Modificar la colección.** El objeto de enumerador devuelto por <xref:System.Collections.IEnumerable.GetEnumerator%2A> normalmente no le permite cambiar la colección agregando, eliminando, reemplazando o reordenar los elementos. Si cambia la colección después de haber iniciado una `For Each`... `Next` bucle, el objeto de enumerador deja de ser válido y el siguiente intento de acceder a un elemento hace que un <xref:System.InvalidOperationException> excepción.  
  
 Sin embargo, este bloqueo de modificación no está determinado por Visual Basic, pero por la implementación de la <xref:System.Collections.IEnumerable> interfaz. Es posible implementar `IEnumerable` de forma que permite la modificación durante la iteración. Si se va a realizar dicha modificación dinámica, asegúrese de que comprende las características de la `IEnumerable` implementación en la colección que está utilizando.  
  
 **Modificar elementos de la colección.** El <xref:System.Collections.IEnumerator.Current%2A> es propiedad del objeto enumerador [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md), y devuelve una copia local de cada elemento de la colección. Esto significa que no se puede modificar los propios elementos en un `For Each`... `Next` bucle. Cualquier modificación realizada afecta solo a la copia local de `Current` y no se reflejan en la colección subyacente. Sin embargo, si un elemento es un tipo de referencia, puede modificar los miembros de la instancia a la que señala. En el ejemplo siguiente se modifica el `BackColor` miembro de cada `thisControl` elemento. Sin embargo, no es posible, modificar `thisControl` propio.  
  
```vb  
Sub lightBlueBackground(ByVal thisForm As System.Windows.Forms.Form)  
    For Each thisControl As System.Windows.Forms.Control In thisForm.Controls  
        thisControl.BackColor = System.Drawing.Color.LightBlue  
    Next thisControl  
End Sub  
```  
  
 En el ejemplo anterior se puede modificar el `BackColor` miembro de cada `thisControl` elemento, aunque no puede modificar `thisControl` propio.  
  
 **Recorrer las matrices.** Dado que el <xref:System.Array> la clase implementa la <xref:System.Collections.IEnumerable> exponen todas las matrices de interfaz, el <xref:System.Array.GetEnumerator%2A> método. Esto significa que puede iterar a través de una matriz con un `For Each`... `Next` bucle. Sin embargo, solo puede leer los elementos de matriz. No se pueden cambiar.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se enumeran todas las carpetas en el directorio C:\ utilizando la <xref:System.IO.DirectoryInfo> clase.  
  
 [!code-vb[VbVbalrStatements#124](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#124)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra un procedimiento para ordenar una colección. El ejemplo ordena las instancias de un `Car` clase que se almacenan en un <xref:System.Collections.Generic.List%601>. La clase `Car` implementa la interfaz <xref:System.IComparable%601>, que requiere implementar el método <xref:System.IComparable%601.CompareTo%2A>.  
  
 Cada llamada a la <xref:System.IComparable%601.CompareTo%2A> método realiza una comparación única que se utiliza para ordenar. El código escrito por el usuario en el método `CompareTo` devuelve un valor para cada comparación del objeto actual con otro objeto. El valor devuelto es menor que cero si el objeto actual es menor que el otro objeto, mayor que cero si el objeto actual es mayor que el otro objeto y cero si son iguales. Esto permite definir en el código los criterios de mayor que, menor que e igual.  
  
 En el método `ListCars`, la instrucción `cars.Sort()` ordena la lista. Esta llamada al método <xref:System.Collections.Generic.List%601.Sort%2A> de <xref:System.Collections.Generic.List%601> hace que se llame automáticamente al método `CompareTo` para los objetos `Car` de `List`.  
  
 [!code-vb[VbVbalrStatements#125](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class9.vb#125)]  
  
## <a name="see-also"></a>Vea también

- [Colecciones](../../../standard/collections/index.md)
- [For...Next (instrucción)](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [Estructuras de bucle](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)
- [While...End While (instrucción)](../../../visual-basic/language-reference/statements/while-end-while-statement.md)
- [Do...Loop (instrucción)](../../../visual-basic/language-reference/statements/do-loop-statement.md)
- [Conversiones de ampliación y de restricción](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
- [Inicializadores de objeto: Tipos con nombre y anónimos](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [Inicializadores de colección](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)
- [Matrices](../../../visual-basic/programming-guide/language-features/arrays/index.md)
