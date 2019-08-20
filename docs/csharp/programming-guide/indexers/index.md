---
title: 'Indexadores: Guía de programación de C#'
ms.custom: seodec18
ms.date: 03/10/2017
f1_keywords:
- cs.indexers
helpviewer_keywords:
- indexers [C#]
- C# language, indexers
ms.assetid: 022cd27d-d5e0-4cfe-8b97-dc018cc3355d
ms.openlocfilehash: 130cc68906be433afc906cfb22759f4ae3dba447
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589449"
---
# <a name="indexers-c-programming-guide"></a>Indizadores (Guía de programación de C#)

Los indizadores permiten indizar las instancias de una clase o struct como matrices. El valor indizado se puede establecer o recuperar sin especificar explícitamente un miembro de tipo o de instancia. Son similares a [propiedades](../classes-and-structs/properties.md), excepto en que sus descriptores de acceso usan parámetros.  
 
 En el ejemplo siguiente se define una clase genérica con métodos de descriptor de acceso [get](../../language-reference/keywords/get.md) y [set](../../language-reference/keywords/set.md) sencillos para asignar y recuperar valores. La clase `Program` crea una instancia de esta clase para almacenar cadenas.  
  
 [!code-csharp[indexers#1](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-1.cs)]  
  
> [!NOTE]
>  Para obtener más ejemplos, vea [Secciones relacionadas](./index.md#BKMK_RelatedSections).  
  
## <a name="expression-body-definitions"></a>Definiciones de cuerpos de expresión  
 
Es habitual que un descriptor de acceso get o set de un indizador conste de una única instrucción que devuelve o establece un valor. Los miembros con forma de expresión proporcionan una sintaxis simplificada para admitir este escenario. A partir de C# 6, un indizador de solo lectura puede implementarse como un miembro con forma de expresión, como se muestra en el ejemplo siguiente.

[!code-csharp[indexers#2](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-2.cs)]  

Tenga en cuenta que `=>` presenta el cuerpo de la expresión y que la palabra clave `get` no se utiliza. 

A partir de C# 7.0, los descriptores de acceso get y set se pueden implementar como miembros con forma de expresión. En este caso, sí deben utilizarse las palabras clave `get` y `set`. Por ejemplo:

[!code-csharp[indexers#3](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-3.cs)]  
  
## <a name="indexers-overview"></a>Información general sobre los indizadores  
  
- Los indizadores permiten indizar objetos de manera similar a como se hace con las matrices.  
  
- Un descriptor de acceso `get` devuelve un valor. Un descriptor de acceso `set` asigna un valor.  
  
- La palabra clave [this](../../language-reference/keywords/this.md) se usa para definir los indizadores.  
  
- La palabra clave [value](../../language-reference/keywords/value.md) se usa para definir el valor asignado por el indizador `set`.  
  
- Los indizadores no tienen que ser indizados por un valor entero; depende de usted cómo definir el mecanismo de búsqueda concreto.  
  
- Los indizadores se pueden sobrecargar.  
  
- Los indizadores pueden tener más de un parámetro formal, por ejemplo, al tener acceso a una matriz bidimensional.  
  
## <a name="BKMK_RelatedSections"></a> Secciones relacionadas  
  
- [Utilizar indizadores](./using-indexers.md)  
  
- [Indizadores en Interfaces](./indexers-in-interfaces.md)  
  
- [Comparación entre propiedades e indizadores](./comparison-between-properties-and-indexers.md)  
  
- [Restringir la accesibilidad del descriptor de acceso](../classes-and-structs/restricting-accessor-accessibility.md)  
  
## <a name="c-language-specification"></a>Especificación del lenguaje C#  

Para obtener más información, vea la sección [Indizadores](~/_csharplang/spec/classes.md#indexers) de [Especificación del lenguaje C#](../../language-reference/language-specification/index.md). La especificación del lenguaje es la fuente definitiva de la sintaxis y el uso de C#.
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../index.md)
- [Propiedades](../classes-and-structs/properties.md)
