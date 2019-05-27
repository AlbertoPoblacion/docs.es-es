---
title: 'Utilizar espacios de nombres: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- cs.names
helpviewer_keywords:
- fully qualified names [C#]
- namespaces [C#], how to use
ms.assetid: 1fe8bf39-addc-438a-bd9e-86410e32381d
ms.openlocfilehash: c5bede7475fdbee3f3524984a9be97b95b44817d
ms.sourcegitcommit: 4c10802ad003374641a2c2373b8a92e3c88babc8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2019
ms.locfileid: "65452683"
---
# <a name="using-namespaces-c-programming-guide"></a>Utilizar espacios de nombres (Guía de programación de C#)
Los espacios de nombres se usan mucho en programas de C# de dos maneras. En primer lugar, las clases de .NET Framework usan espacios de nombres para organizar sus clases. En segundo lugar, declarar sus propios espacios de nombres puede ayudar a controlar el ámbito de nombres de clase y método en proyectos de programación grandes.  
  
## <a name="accessing-namespaces"></a>Acceder a los espacios de nombres  
 La mayoría de las aplicaciones de C# comienzan con una sección de directivas `using`. En esta sección se muestran los espacios de nombres que la aplicación usará frecuentemente, y evita que el programador especifique un nombre completo cada vez que se use un método que se incluye dentro.  
  
 Por ejemplo, incluyendo la línea:  
  
 [!code-csharp[csProgGuide#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/using.cs#1)]  
  
 Al comienzo de un programa, el programador puede usar el código:  
  
 [!code-csharp[csProgGuide#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#31)]  
  
 En lugar de:  
  
 [!code-csharp[csProgGuide#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuide/CS/progGuide.cs#30)]  
  
## <a name="namespace-aliases"></a>Alias de espacios de nombres  
 La [directiva Using](../../../csharp/language-reference/keywords/using-directive.md) también puede usarse para crear un alias para un [espacio de nombres](../../../csharp/language-reference/keywords/namespace.md). Por ejemplo, si está usando un espacio de nombres escrito previamente que contiene espacios de nombres anidados, puede que quiera declarar un alias para proporcionar una manera abreviada de hacer referencia a uno en concreto, como se muestra en el ejemplo siguiente:  
  
 [!code-csharp[csProgGuideNamespaces#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces2.cs#7)]  
  
## <a name="using-namespaces-to-control-scope"></a>Usar los espacios de nombres para controlar el ámbito  
 La palabra clave `namespace` se usa para declarar un ámbito. La capacidad de crear ámbitos en su proyecto le ayuda a organizar código y le permite crear tipos únicos globalmente. En el ejemplo siguiente, una clase denominada `SampleClass` se define en dos espacios de nombres, uno anidado dentro de otro. El [operador `.` de acceso a miembros](../../language-reference/operators/member-access-operators.md#member-access-operator-) se utiliza para diferenciar el método al que se llama.  
  
 [!code-csharp[csProgGuideNamespaces#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#8)]  
  
## <a name="fully-qualified-names"></a>nombres completos  
 Los espacios de nombres y los tipos tienen títulos únicos descritos mediante nombres completos que indican una jerarquía lógica. Por ejemplo, la instrucción `A.B` implica que `A` es el nombre del espacio de nombres o el tipo, y `B` está anidado en su interior.  
  
 En el ejemplo siguiente, existen espacios de nombres y clases anidadas. El nombre completo se indica como un comentario que sigue a cada entidad.  
  
 [!code-csharp[csProgGuideNamespaces#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#9)]  
  
 En el segmento de código anterior:  
  
- El espacio de nombres `N1` es un miembro del espacio de nombres global. Su nombre completo es `N1`.  
  
- El espacio de nombres `N2` es un miembro de `N1`. Su nombre completo es `N1.N2`.  
  
- La clase `C1` es un miembro de `N1`. Su nombre completo es `N1.C1`.  
  
- El nombre de la clase `C2` se usa dos veces en este código. En cambio, los nombres completos son únicos. La primera instancia de `C2` se declara dentro de `C1`; por lo tanto, su nombre completo es: `N1.C1.C2`. La segunda instancia de `C2` se declara dentro de un espacio de nombres `N2`; por lo tanto, su nombre completo es `N1.N2.C2`.  
  
 Con el segmento de código anterior, puede agregar un nuevo miembro de clase, `C3`, al espacio de nombres `N1.N2` de la manera siguiente:  
  
 [!code-csharp[csProgGuideNamespaces#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#10)]  
  
 En general, use `::` para hacer referencia a un alias de espacio de nombres o `global::` para hacer referencia al espacio de nombres global y `.` para calificar tipos o miembros.  
  
 Es un error usar `::` con un alias que haga referencia a un tipo en lugar de a un espacio de nombres. Por ejemplo:  
  
 [!code-csharp[csProgGuideNamespaces#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces2.cs#11)]  
  
 [!code-csharp[csProgGuideNamespaces#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces2.cs#12)]  
  
 Recuerde que la palabra `global` no es un alias predefinido; por lo tanto, `global.X` no tiene ningún significado especial. Adquiere un significado especial solo cuando se usa con `::`.  
  
 La advertencia del compilador CS0440 se genera si define un alias denominado global porque `global::` siempre hace referencia al espacio de nombres global y no a un alias. Por ejemplo, la línea siguiente genera la advertencia:  
  
 [!code-csharp[csProgGuideNamespaces#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces2.cs#13)]  
  
 Usar `::` con alias es una buena idea y protege contra la introducción inesperada de tipos adicionales. Por ejemplo, considere este ejemplo:  
  
 [!code-csharp[csProgGuideNamespaces#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#14)]  
  
 [!code-csharp[csProgGuideNamespaces#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideNamespaces/CS/Namespaces.cs#15)]  
  
 Esto funciona, pero si un tipo denominado `Alias` fuera a introducirse posteriormente, `Alias.` se enlazaría a ese tipo en su lugar. Usar `Alias::Exception` garantiza que `Alias` se trata como un alias de espacio de nombres y no se confunde con un tipo.  
  
 Vea el tema [Cómo: Usar el alias del espacio de nombres global](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md) para obtener más información sobre el alias `global`.  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Espacios de nombres](../../../csharp/programming-guide/namespaces/index.md)
- [Palabras clave del espacio de nombres](../../../csharp/language-reference/keywords/namespace-keywords.md)
- [. !](../../../csharp/language-reference/operators/member-access-operators.md#member-access-operator-)
- [:: !](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)
- [extern](../../../csharp/language-reference/keywords/extern.md)
