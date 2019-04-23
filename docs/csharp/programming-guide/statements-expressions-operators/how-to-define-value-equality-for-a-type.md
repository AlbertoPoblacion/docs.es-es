---
title: 'Procedimiento Definir la igualdad de valores para un tipo: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- overriding Equals method [C#]
- object equivalence [C#]
- Equals method [C#], overriding
- value equality [C#]
- equivalence [C#]
ms.assetid: 4084581e-b931-498b-9534-cf7ef5b68690
ms.openlocfilehash: 73cb9249343b02c937c3e4e652021c7a6dbb4386
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59311479"
---
# <a name="how-to-define-value-equality-for-a-type-c-programming-guide"></a>Procedimiento Definir la igualdad de valores para un tipo (Guía de programación de C#)
Cuando defina una clase o un struct, debe decidir si tiene sentido crear una definición personalizada de igualdad (o equivalencia) de valores para el tipo. Normalmente, la igualdad de valores se implementa cuando se espera agregar objetos del tipo a una colección de algún tipo, o cuando su objetivo principal es almacenar un conjunto de campos o propiedades. Puede basar la definición de la igualdad de valores en una comparación de todos los campos y propiedades del tipo, o bien puede basarla en un subconjunto. En cualquier caso, y tanto en las clases como en los structs, la implementación debe cumplir las cinco garantías de equivalencia:  
  
1. `x.Equals(x)` devuelve `true`. Esto se denomina propiedad reflexiva.  
  
2. `x.Equals(y)` devuelve el mismo valor que `y.Equals(x)`. Esto se denomina propiedad simétrica.  
  
3. Si `(x.Equals(y) && y.Equals(z))` devuelve `true`, `x.Equals(z)` devuelve `true`. Esto se denomina propiedad transitiva.  
  
4. Las invocaciones sucesivas de `x.Equals(y)` devuelven el mismo valor siempre y cuando los objetos a los que x e y hacen referencia no se modifiquen.  
  
5. `x.Equals(null)` devuelve `false`. Pero `null.Equals(null)` produce una excepción; no cumple la regla anterior número dos.  
  
 Cualquier struct que defina ya tiene una implementación predeterminada de igualdad de valor que hereda de la invalidación <xref:System.ValueType?displayProperty=nameWithType> del método <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType>. Esta implementación usa la reflexión para examinar todos los campos y propiedades del tipo. Aunque esta implementación genera resultados correctos, es relativamente lenta en comparación con una implementación personalizada escrita específicamente para el tipo.  
  
 Los detalles de implementación para la igualdad de valores son diferentes para las clases y los structs. A pesar de ello, tanto las clases como los structs requieren los mismos pasos básicos para implementar la igualdad:  
  
1. Invalide el método <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> [virtual](../../../csharp/language-reference/keywords/virtual.md). En la mayoría de los casos, la implementación de `bool Equals( object obj )` debería llamar solamente al método `Equals` específico del tipo que es la implementación de la interfaz <xref:System.IEquatable%601?displayProperty=nameWithType>. (Vea el paso 2).  
  
2. Implemente la interfaz <xref:System.IEquatable%601?displayProperty=nameWithType> proporcionando un método `Equals` específico del tipo. Aquí es donde se realiza la comparación de equivalencias propiamente dicha. Por ejemplo, podría decidir que, para definir la igualdad, solo se comparen uno o dos campos del tipo. No genere excepciones desde `Equals`. Solo para las clases: este método debe examinar únicamente los campos que se declaran en la clase. Debe llamar a `base.Equals` para examinar los campos que están en la clase base. (No realice esto si el tipo hereda directamente de <xref:System.Object>, porque la implementación <xref:System.Object> de <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> realiza una comprobación de igualdad de referencia).  
  
3. Opcional, pero recomendado: Sobrecargue los operadores [==](../../../csharp/language-reference/operators/equality-operators.md#equality-operator-) y [!=](../../../csharp/language-reference/operators/equality-operators.md#inequality-operator-).  
  
4. Invalide <xref:System.Object.GetHashCode%2A?displayProperty=nameWithType> de manera que dos objetos que tengan igualdad de valor produzcan el mismo código hash.  
  
5. Opcional: Para admitir definiciones para "mayor que" o "menor que", implemente la interfaz <xref:System.IComparable%601> para el tipo y sobrecargue también los operadores [<=](../../../csharp/language-reference/operators/less-than-equal-operator.md) y [>=](../../../csharp/language-reference/operators/greater-than-equal-operator.md).  
  
 En el primer ejemplo que aparece más abajo se muestra una implementación de clase. En el segundo ejemplo se muestra una implementación de struct.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo implementar la igualdad de valores en una clase (tipo de referencia).  
  
 [!code-csharp[csProgGuideStatements#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#19)]  
  
 En las clases (tipos de referencia), la implementación predeterminada de ambos métodos <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> realiza una comparación de igualdad de referencia, no una comprobación de igualdad de valores. Cuando un implementador invalida el método virtual, lo hace para asignarle semántica de igualdad de valores.  
  
 Los operadores `==` y `!=` pueden usarse con clases, incluso si la clase no los sobrecarga, pero el comportamiento predeterminado consiste en realizar una comprobación de igualdad de referencia. En una clase, si sobrecarga el método `Equals`, debería sobrecargar los operadores `==` y `!=`, pero no es obligatorio.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo implementar la igualdad de valores en un struct (tipo de valor):  
  
 [!code-csharp[csProgGuideStatements#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#20)]  
  
 Para los structs, la implementación predeterminada de <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> (que es la versión invalidada de <xref:System.ValueType?displayProperty=nameWithType>) realiza una comprobación de igualdad de valor con la reflexión para comparar valores de cada campo en el tipo. Cuando un implementador invalida el método `Equals` virtual en un struct, lo hace para proporcionar un medio más eficaz de llevar a cabo la comprobación de igualdad de valores y, opcionalmente, para basar la comparación en un subconjunto de propiedades o campos del struct.  
  
 Los operadores [==](../../../csharp/language-reference/operators/equality-operators.md#equality-operator-) y [!=](../../../csharp/language-reference/operators/equality-operators.md#inequality-operator-) no pueden funcionar en un struct a menos que el struct los sobrecargue explícitamente.  
  
## <a name="see-also"></a>Vea también

- [Comparaciones de igualdad](../../../csharp/programming-guide/statements-expressions-operators/equality-comparisons.md)
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
