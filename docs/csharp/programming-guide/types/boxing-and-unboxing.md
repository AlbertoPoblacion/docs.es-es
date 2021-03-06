---
title: 'Conversión boxing y unboxing: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- cs.boxing
helpviewer_keywords:
- C# language, boxing
- C# language, unboxing
- unboxing [C#]
- boxing [C#]
ms.assetid: 8da9bbf4-bce9-4b08-b2e5-f64c11c56514
ms.openlocfilehash: 4fdaea6a9b69f50fa61ee40a43bf34953e72cef1
ms.sourcegitcommit: bdd930b5df20a45c29483d905526a2a3e4d17c5b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53237342"
---
# <a name="boxing-and-unboxing-c-programming-guide"></a>Conversión boxing y unboxing (Guía de programación de C#)
La conversión boxing es el proceso de convertir un [tipo de valor](../../../csharp/language-reference/keywords/value-types.md) en el tipo `object` o en cualquier tipo de interfaz implementado por este tipo de valor. Cuando CLR aplica la conversión boxing a un tipo de valor, ajusta el valor dentro de una clase System.Object y lo almacena en el montón administrado. La conversión unboxing extrae el tipo de valor del objeto. La conversión boxing es implícita y la conversión unboxing es explícita. El concepto de conversión boxing y unboxing es la base de la vista unificada del sistema de tipos de C#, en el que un valor de cualquier tipo se puede tratar como objeto.  
  
 En el ejemplo siguiente, se aplica *conversión boxing* a la variable de entero `i` y esta se asigna al objeto `o`.  
  
 [!code-csharp[csProgGuideTypes#14](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_1.cs)]  
  
 Luego se puede aplicar conversión unboxing al objeto `o` y asignarlo a la variable de entero `i`:  
  
 [!code-csharp[csProgGuideTypes#15](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_2.cs)]  
  
 En los ejemplos siguientes se muestra cómo usar la conversión boxing en C#.  
  
 [!code-csharp[csProgGuideTypes#47](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_3.cs)]  
  
## <a name="performance"></a>Rendimiento  
 Con relación a las asignaciones simples, las conversiones boxing y unboxing son procesos que consumen muchos recursos. Cuando se aplica la conversión boxing a un tipo de valor, se debe asignar y construir un objeto completamente nuevo. En menor grado, la conversión de tipos requerida para aplicar la conversión unboxing también es costosa. Para más información, vea [Rendimiento](../../../../docs/framework/performance/performance-tips.md).  
  
## <a name="boxing"></a>Boxing  
 La conversión boxing se utiliza para almacenar tipos de valor en el montón de recolección de elementos no utilizados. La conversión boxing es una conversión implícita de un [tipo de valor](../../../csharp/language-reference/keywords/value-types.md) en el tipo `object` o en cualquier tipo de interfaz implementado por este tipo de valor. Al aplicar la conversión boxing a un tipo de valor se asigna una instancia de objeto en el montón y se copia el valor en el nuevo objeto.  
  
 Considere la siguiente declaración de una variable de tipo de valor:  
  
 [!code-csharp[csProgGuideTypes#17](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_4.cs)]  
  
 La siguiente instrucción aplica implícitamente la operación de conversión boxing en la variable `i`:  
  
 [!code-csharp[csProgGuideTypes#18](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_5.cs)]  
  
 El resultado de esta instrucción es crear una referencia de objeto `o` en la pila que hace referencia a un valor del tipo `int` en el montón. Este valor es una copia del tipo de valor asignado a la variable `i`. La diferencia entre las dos variables, `i` y `o`, se muestra en la figura siguiente.  
  
 ![Gráfico BoxingConversion](../../../csharp/programming-guide/types/media/vcboxingconversion.gif "vcBoxingConversion")  
Conversión boxing  
  
 También es posible realizar la conversión boxing de manera explícita, tal como se muestra en el ejemplo siguiente, pero esta nunca es necesaria:  
  
 [!code-csharp[csProgGuideTypes#19](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_6.cs)]  
  
## <a name="description"></a>Descripción  
 Este ejemplo convierte una variable de entero `i` en un objeto `o` mediante la conversión boxing. A continuación, el valor almacenado en la variable `i` se cambia de `123` a `456`. El ejemplo muestra que el tipo de valor original y el objeto al que se ha aplicado la conversión boxing usan ubicaciones de memoria independientes y, por consiguiente, pueden almacenar valores diferentes.  
  
## <a name="example"></a>Ejemplo  
 [!code-csharp[csProgGuideTypes#16](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_7.cs)]  
  
## <a name="unboxing"></a>Conversión unboxing  
 La conversión unboxing es una conversión explícita del tipo `object` en un [tipo de valor](../../../csharp/language-reference/keywords/value-types.md) o de un tipo de interfaz en un tipo de valor que implementa la interfaz. Una operación de conversión unboxing consiste en lo siguiente:  
  
-   Comprobar la instancia de objeto para asegurarse de que se trata de un valor de conversión boxing del tipo de valor dado.  
  
-   Copiar el valor de la instancia en la variable de tipo de valor.  
  
 Las siguientes instrucciones muestran las operaciones de conversión boxing y unboxing:  
  
 [!code-csharp[csProgGuideTypes#21](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_8.cs)]  
  
 En la figura siguiente se muestra el resultado de las instrucciones anteriores.  
  
 ![Gráfico de conversión unboxing](../../../csharp/programming-guide/types/media/vcunboxingconversion.gif "vcUnBoxingConversion")  
Conversión unboxing  
  
 Para que la conversión unboxing de tipos de valor sea correcta en tiempo de ejecución, el elemento al que se aplica debe ser una referencia a un objeto creado previamente mediante la conversión boxing de una instancia de ese tipo de valor. Si se intenta aplicar la conversión unboxing a `null`, se producirá una excepción <xref:System.NullReferenceException>. Si se intenta aplicar la conversión unboxing a una referencia de un tipo de valor incompatible, se producirá una excepción <xref:System.InvalidCastException>.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra un caso de conversión unboxing no válida y la excepción `InvalidCastException` resultante. Si se utiliza `try` y `catch`, se muestra un mensaje de error cuando se produce el error.  
  
 [!code-csharp[csProgGuideTypes#20](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/boxing-and-unboxing_9.cs)]  
  
 Este programa produce el resultado siguiente:  
  
 `Specified cast is not valid. Error: Incorrect unboxing.`  
  
 Si cambia la instrucción:  
  
```csharp
int j = (short) o;  
```  
  
 a:  
  
```csharp
int j = (int) o;  
```  
  
 la conversión se realizará y se obtendrá el resultado:  
  
 `Unboxing OK.`  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="related-sections"></a>Secciones relacionadas  
 Para obtener más información:  
  
-   [Tipos de referencia](../../../csharp/language-reference/keywords/reference-types.md)  
  
-   [Tipos de valor](../../../csharp/language-reference/keywords/value-types.md)  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
