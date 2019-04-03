---
title: Function (Instrucción, Visual Basic)
ms.date: 05/12/2018
f1_keywords:
- vb.Function
helpviewer_keywords:
- procedures [Visual Basic], creating
- Function procedures [Visual Basic], Function statement syntax
- functions [Visual Basic], function procedures
- ParamArray keyword [Visual Basic], Function statements
- Private keyword [Visual Basic], Function statements
- declarations [Visual Basic], procedures
- procedures [Visual Basic], declaration
- Public keyword [Visual Basic], in Function statement
- ByVal keyword [Visual Basic], Function statements
- procedures [Visual Basic], recursive
- Implements keyword [Visual Basic], Function statements
- procedures [Visual Basic], returning values
- Exit statement [Visual Basic], in Function procedures
- recursive procedures
- As keyword [Visual Basic], in Function statement
- Optional keyword [Visual Basic], Function statements
- Function statement [Visual Basic]
- Visual Basic code, Function procedures
- procedures [Visual Basic], function
- ByRef keyword [Visual Basic], Function statements
- Friend keyword [Visual Basic], Function statements
- End keyword [Visual Basic], Function statements
- Handles keyword [Visual Basic], Function statements
ms.assetid: a4497077-0f46-4ede-a27f-9e8670df52b9
ms.openlocfilehash: dffe67d1c31b0fe7c037839ba0588793a461f276
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58818467"
---
# <a name="function-statement-visual-basic"></a>Function (Instrucción, Visual Basic)
Declara el nombre, parámetros y código que definen un `Function` procedimiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
[ <attributelist> ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async | Iterator ]  
Function name [ (Of typeparamlist) ] [ (parameterlist) ] [ As returntype ] [ Implements implementslist | Handles eventlist ]  
    [ statements ]  
    [ Exit Function ]  
    [ statements ]  
End Function  
```  
  
## <a name="parts"></a>Elementos  
  
-   `attributelist`  
  
     Opcional. Consulte [lista de los atributos](attribute-list.md).  
  
-   `accessmodifier`  
  
     Opcional. Puede ser uno de los siguientes:  
  
    -   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Private](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   [Protected Friend](../../language-reference/modifiers/protected-friend.md)

    - [Private Protected](../../language-reference/modifiers/private-protected.md)  
  
     Vea [Access levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
-   `proceduremodifiers`  
  
     Opcional. Puede ser uno de los siguientes:  
  
    -   [Sobrecargas](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
    -   [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)  
  
    -   [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)  
  
    -   [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
  
    -   [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
  
    -   `MustOverride Overrides`  
  
    -   `NotOverridable Overrides`  
  
-   `Shared`  
  
     Opcional. Consulte [compartido](../../../visual-basic/language-reference/modifiers/shared.md).  
  
-   `Shadows`  
  
     Opcional. Consulte [sombras](../../../visual-basic/language-reference/modifiers/shadows.md).  
  
-   `Async`  
  
     Opcional. Consulte [Async](../../../visual-basic/language-reference/modifiers/async.md).  
  
-   `Iterator`  
  
     Opcional. Consulte [iterador](../../../visual-basic/language-reference/modifiers/iterator.md).  
  
-   `name`  
  
     Obligatorio. Nombre del procedimiento. Vea [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   `typeparamlist`  
  
     Opcional. Lista de parámetros de tipo para un procedimiento genérico. Consulte [escriba lista](type-list.md).  
  
-   `parameterlist`  
  
     Opcional. Lista de nombres de variables locales que representan los parámetros de este procedimiento. Consulte [Lista_de_parámetros](parameter-list.md).  
  
-   `returntype`  
  
     Es necesario si `Option Strict` es `On`. Tipo de datos del valor devuelto por este procedimiento.  
  
-   `Implements`  
  
     Opcional. Indica que este procedimiento implementa uno o varios `Function` procedimientos, cada uno definido en una interfaz implementada por la clase o estructura contenedora de este procedimiento. Consulte [implementa instrucción](implements-statement.md).  
  
-   `implementslist`  
  
     Es necesario si se proporciona `Implements`. Lista de procedimientos `Function` que se implementan.  
  
     `implementedprocedure [ , implementedprocedure ... ]`  
  
     Cada `implementedprocedure` tiene la sintaxis y las partes siguientes:  
  
     `interface.definedname`  
  
    |Parte|Descripción|  
    |---|---|  
    |`interface`|Obligatorio. Nombre de una interfaz implementada por este procedimiento contenedora de clase o estructura.|  
    |`definedname`|Obligatorio. Nombre por el que se define el procedimiento en `interface`.|  
  
-   `Handles`  
  
     Opcional. Indica que este procedimiento puede controlar uno o más eventos específicos. Consulte [controla](handles-clause.md).  
  
-   `eventlist`  
  
     Es necesario si se proporciona `Handles`. Lista de eventos que controla este procedimiento.  
  
     `eventspecifier [ , eventspecifier ... ]`  
  
     Cada `eventspecifier` tiene la sintaxis y las partes siguientes:  
  
     `eventvariable.event`  
  
    |Parte|Descripción|  
    |---|---|  
    |`eventvariable`|Obligatorio. Variable de objeto declarada con el tipo de datos de la clase o estructura que provoca el evento.|  
    |`event`|Obligatorio. Nombre del evento que controla este procedimiento.|  
  
-   `statements`  
  
     Opcional. Bloque de instrucciones que se ejecutan dentro de este procedimiento.  
  
-   `End Function`  
  
     Termina la definición de este procedimiento.  
  
## <a name="remarks"></a>Comentarios  
 El código ejecutable debe estar dentro de un procedimiento. A su vez, cada procedimiento, se declara dentro de una clase, una estructura o un módulo que se conoce como la clase, estructura o módulo que lo contiene.  
  
 Para devolver un valor al código de llamada, use un `Function` procedimiento; en caso contrario, use un `Sub` procedimiento.  
  
## <a name="defining-a-function"></a>Definir una función  
 Puede definir un `Function` procedimiento sólo en el nivel de módulo. Por lo tanto, el contexto de declaración de una función debe ser una clase, una estructura, un módulo o una interfaz y no puede ser un archivo de código fuente, un espacio de nombres, un procedimiento o un bloque. Para obtener más información, vea [Declaration Contexts and Default Access Levels](declaration-contexts-and-default-access-levels.md) (Contextos de declaración y niveles de acceso predeterminados).  
  
 `Function` valor predeterminado de los procedimientos para acceso público. Los niveles de acceso se pueden ajustar con los modificadores de acceso.  
  
 Un `Function` procedimiento puede declarar el tipo de datos del valor que devuelve el procedimiento. Puede especificar cualquier tipo de datos o el nombre de una enumeración, una estructura, una clase o una interfaz. Si no se especifica la `returntype` parámetro, el procedimiento devuelve `Object`.  
  
 Si este procedimiento utiliza el `Implements` también debe tener la palabra clave, la clase o estructura que contiene un `Implements` instrucción que sigue inmediatamente a su `Class` o `Structure` instrucción. El `Implements` instrucción debe incluir cada interfaz que se especifica en `implementslist`. Sin embargo, el nombre por el que una interfaz define el `Function` (en `definedname`) no tiene que coincidir con el nombre de este procedimiento (en `name`).  
  
> [!NOTE]
>  Puede usar expresiones lambda para definir expresiones de función en línea. Para obtener más información, consulte [expresión de función](../../../visual-basic/language-reference/operators/function-expression.md) y [expresiones Lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).  
  
## <a name="returning-from-a-function"></a>Devolver desde una función  
 Cuando el `Function` procedimiento vuelve al código de llamada, la ejecución continúa con la instrucción que sigue a la instrucción que llamó al procedimiento.  
  
 Para devolver un valor de una función, puede asignar el valor al nombre de función o incluirlo en un `Return` instrucción.  
  
 El `Return` instrucción asigna el valor devuelto al mismo tiempo y sale de la función, como se muestra en el ejemplo siguiente.  
  
 [!code-vb[VbVbalrStatements#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#24)]  
  
 En el ejemplo siguiente se asigna el valor devuelto para el nombre de función `myFunction` y, a continuación, usa el `Exit Function` instrucción para devolver.  
  
 [!code-vb[VbVbalrStatements#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#23)]  
  
 El `Exit Function` y `Return` instrucciones provocan una inmediata salida desde un `Function` procedimiento. Cualquier número de `Exit Function` y `Return` instrucciones pueden aparecer en cualquier lugar en el procedimiento, y puede mezclar `Exit Function` y `Return` instrucciones.  
  
 Si usas `Exit Function` sin asignar un valor a `name`, el procedimiento devuelve el valor predeterminado para el tipo de datos que se especifica en `returntype`. Si `returntype` no se especifica, el procedimiento devuelve `Nothing`, que es el valor predeterminado de `Object`.  
  
## <a name="calling-a-function"></a>Llamar a una función  
 Se llama a un `Function` procedimiento utilizando el nombre del procedimiento, seguido de la lista de argumentos entre paréntesis en una expresión. Puede omitir los paréntesis solo si no se proporciona ningún argumento. Sin embargo, el código es más legible si siempre incluye los paréntesis.  
  
 Se llama a un `Function` procedimiento del mismo modo que llamar a cualquier biblioteca de función como `Sqrt`, `Cos`, o `ChrW`.  
  
 También puede llamar a una función mediante el `Call` palabra clave. En ese caso, se omite el valor devuelto. El uso de la `Call` palabra clave no se recomienda en la mayoría de los casos. Para obtener más información, consulte [instrucción Call](call-statement.md).  
  
 Visual Basic a veces se reorganiza las expresiones aritméticas para aumentar la eficacia interna. Por ese motivo, no debe usar un `Function` procedimiento en una expresión aritmética cuando la función cambia el valor de variables en la misma expresión.  
  
## <a name="async-functions"></a>Funciones asincrónicas  
 El *Async* característica permite invocar las funciones asincrónicas sin usar devoluciones de llamada explícitas ni dividir manualmente el código en varias funciones o expresiones lambda.  
  
 Si marca una función con el [Async](../../../visual-basic/language-reference/modifiers/async.md) modificador, puede usar el [Await](../../../visual-basic/language-reference/operators/await-operator.md) operador en la función. Cuando el control alcanza un `Await` expresión en el `Async` función, el control vuelve al llamador y progreso de la función se suspende hasta que se complete la tarea esperada. Cuando se completa la tarea, puede reanudar la ejecución de la función.  
  
> [!NOTE]
>  Un `Async` procedimiento vuelve al llamador cuando encuentra el primer objeto esperado que aún no se ha completado, o cuando llega al final de la `Async` procedimiento, lo que ocurra primero.  
  
 Un `Async` función puede tener un tipo de valor devuelto de <xref:System.Threading.Tasks.Task%601> o <xref:System.Threading.Tasks.Task>. Un ejemplo de un `Async` función que tiene un tipo de valor devuelto de <xref:System.Threading.Tasks.Task%601> se proporciona a continuación.  
  
 Un `Async` función no puede declarar ningún [ByRef](../../../visual-basic/language-reference/modifiers/byref.md) parámetros.  
  
 Un [Sub (instrucción)](sub-statement.md) también se pueden marcar con el `Async` modificador. Se utiliza principalmente para controladores de eventos, donde no se puede devolver un valor. Un `Async` `Sub` procedimiento no se espera y el llamador de un `Async` `Sub` procedimiento no puede detectar las excepciones producidas por la `Sub` procedimiento.  
  
 Para obtener más información acerca de `Async` funciones, vea [programación asincrónica con Async y Await](../../../visual-basic/programming-guide/concepts/async/index.md), [flujo de Control en programas Async](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md), y [tipos de valor devueltos de Async](../../../visual-basic/programming-guide/concepts/async/async-return-types.md).  
  
## <a name="iterator-functions"></a>Funciones de iterador  
 Un *iterador* función realiza una iteración personalizada en una colección, como una lista o matriz. Una función de iterador usa la [Yield](yield-statement.md) instrucción para devolver cada elemento de uno en uno. Cuando un [Yield](yield-statement.md) se alcanza la instrucción, se recuerda la ubicación actual en el código. La ejecución se reinicia desde esa ubicación la próxima vez que se llama a la función del iterador.  
  
 Llamar a un iterador desde código de cliente mediante un [For Each... Siguiente](for-each-next-statement.md) instrucción.  
  
 Puede ser el tipo de valor devuelto de una función de iterador <xref:System.Collections.IEnumerable>, <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.IEnumerator>, o <xref:System.Collections.Generic.IEnumerator%601>.  
  
 Para obtener más información, consulta [Iteradores](../../programming-guide/concepts/iterators.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa el `Function` instrucción para declarar el nombre, parámetros y código que forman el cuerpo de un `Function` procedimiento. El `ParamArray` modificador permite que la función que acepte un número variable de argumentos.  
  
 [!code-vb[VbVbalrStatements#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#25)]  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente invoca la función declarada en el ejemplo anterior.  
  
 [!code-vb[VbVbalrStatements#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#26)]  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, `DelayAsync` es un `Async` `Function` que tiene un tipo de valor devuelto de <xref:System.Threading.Tasks.Task%601>. `DelayAsync` tiene una instrucción `Return` que devuelve un entero. Por lo tanto, la declaración de función de `DelayAsync` debe tener un tipo de valor devuelto de `Task(Of Integer)`. Dado que el tipo de valor devuelto es `Task(Of Integer)`, la evaluación de la `Await` expresión en `DoSomethingAsync` genera un entero. Esto se muestra en esta instrucción: `Dim result As Integer = Await delayTask`.  
  
 El `startButton_Click` procedimiento es un ejemplo de un `Async Sub` procedimiento. Dado que `DoSomethingAsync` es un `Async` (función), la tarea de la llamada a `DoSomethingAsync` debe esperar, como se muestra en la siguiente instrucción: `Await DoSomethingAsync()`. El `startButton_Click` `Sub` procedimiento debe definirse con la `Async` modificador porque tiene un `Await` expresión.  
  
 [!code-vb[csAsyncMethod#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/csasyncmethod/vb/mainwindow.xaml.vb#1)]  
  
## <a name="see-also"></a>Vea también

- [Sub (instrucción)](sub-statement.md)
- [Procedimientos de función](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)
- [Lista de parámetros](parameter-list.md)
- [Dim (instrucción)](dim-statement.md)
- [Call (instrucción)](call-statement.md)
- [Of](of-clause.md)
- [Matrices de parámetros](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)
- [Cómo: Utilizar una clase genérica](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)
- [Solución de problemas de procedimientos](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)
- [Expresiones lambda](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)
- [Expresión de función](../../../visual-basic/language-reference/operators/function-expression.md)
