---
title: 'Pasar parámetros: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- parameters [C#], passing
- passing parameters [C#]
- arguments [C#]
- methods [C#], passing parameters
- C# language, method parameters
ms.assetid: a5c3003f-7441-4710-b8b1-c79de77e0b77
ms.openlocfilehash: 22f58bda5aa5b60248902a4130f3ea9b6caa65cf
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2019
ms.locfileid: "73419124"
---
# <a name="passing-parameters-c-programming-guide"></a>Pasar parámetros (Guía de programación de C#)
En C#, los argumentos se pueden pasar a parámetros por valor o por referencia. El paso de parámetros por referencia permite a los miembros de funciones, métodos, propiedades, indexadores, operadores y constructores cambiar el valor de los parámetros y hacer que ese cambio persista en el entorno de la llamada. Para pasar un parámetro por referencia con la intención de cambiar el valor, use la palabra clave `ref` o `out`. Para pasar un parámetro por referencia con la intención de evitar la copia pero no modificar el valor, use el modificador `in`. En los ejemplos de este tema, para simplificar, solo se usa la palabra clave `ref`. Para obtener más información sobre la diferencia entre `in`, `ref` y `out`, vea [in](../../language-reference/keywords/in-parameter-modifier.md), [ref](../../language-reference/keywords/ref.md) y [out](../../language-reference/keywords/out-parameter-modifier.md).  
  
 En el ejemplo siguiente se muestra la diferencia entre los parámetros de valor y de referencia.  
  
 [!code-csharp[csProgGuideParameters#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideParameters/CS/Parameters.cs#10)]  
  
 Para obtener más información, vea los temas siguientes:  
  
- [Pasar parámetros de tipo de valor](./passing-value-type-parameters.md)  
  
- [Pasar parámetros Reference-Type](./passing-reference-type-parameters.md)  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  

Para obtener más información, vea la sección [Listas de argumentos](~/_csharplang/spec/expressions.md#argument-lists) de [Especificación del lenguaje C#](/dotnet/csharp/language-reference/language-specification/introduction). La especificación del lenguaje es la fuente definitiva de la sintaxis y el uso de C#.
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../index.md)
- [Métodos](./methods.md)
