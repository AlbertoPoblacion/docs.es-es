---
title: 'alias externo: Referencia de C#'
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- alias_CSharpKeyword
helpviewer_keywords:
- extern alias keyword [C#]
- aliases [C#], extern keyword
- aliases, extern keyword
ms.assetid: f487bf4f-c943-4fca-851b-e540c83d9027
ms.openlocfilehash: cfb662203216aa6ca208ceec20d55164c65163dc
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68626649"
---
# <a name="extern-alias-c-reference"></a>alias externo (Referencia de C#)
Es posible que deba hacer referencia a dos versiones de ensamblados que tienen los mismos nombres de tipo completos. Por ejemplo, es posible que tenga que usar dos o más versiones de un ensamblado en la misma aplicación. Mediante el uso de un alias de ensamblado externo, los espacios de nombres de cada ensamblado pueden ajustarse en espacios de nombres de nivel de raíz denominados por el alias, lo que permite que se usen en el mismo archivo.  
  
> [!NOTE]
>  La palabra clave [extern](../../../csharp/language-reference/keywords/extern.md) también se usa como un modificador de método, y declara un método escrito en código no administrado.  
  
 Para hacer referencia a dos ensamblados con los mismos nombres de tipo completos, debe especificarse un alias en un símbolo del sistema, como sigue:  
  
 `/r:GridV1=grid.dll`  
  
 `/r:GridV2=grid20.dll`  
  
 Esto crea los alias externos `GridV1` y `GridV2`. Para usar estos alias desde dentro de un programa, se hace referencia a ellos mediante la palabra clave `extern`. Por ejemplo:  
  
 `extern alias GridV1;`  
  
 `extern alias GridV2;`  
  
 Cada declaración de alias externo introduce un espacio de nombres de nivel de raíz adicional que es semejante al espacio de nombres global (pero que no se encuentra en su interior). Por tanto, se puede hacer referencia a los tipos de cada ensamblado sin ambigüedad mediante su nombre completo, con raíz en el alias de espacio de nombres adecuado.  
  
 En el ejemplo anterior, `GridV1::Grid` sería el control de cuadrícula de `grid.dll`, y `GridV2::Grid` sería el control de cuadrícula de `grid20.dll`.  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Vea también

- [Referencia de C#](../../../csharp/language-reference/index.md)
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Palabras clave de C#](../../../csharp/language-reference/keywords/index.md)
- [:: !](../../../csharp/language-reference/operators/namespace-alias-qualifier.md)
- [/reference (Opciones del compilador de C#)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)
