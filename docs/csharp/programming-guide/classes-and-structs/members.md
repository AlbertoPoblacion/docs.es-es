---
title: 'Miembros: Guía de programación de C#'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- types [C#], nested types
- C# language, type members
ms.assetid: 4a30a4ab-d690-4936-9124-92ce9448665a
ms.openlocfilehash: affe2752712bfd40516861abf84bdee11528168c
ms.sourcegitcommit: eaa6d5cd0f4e7189dbe0bd756e9f53508b01989e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2019
ms.locfileid: "67609490"
---
# <a name="members-c-programming-guide"></a>Miembros (Guía de programación de C#)

Las clases y structs tienen miembros que representan sus datos y comportamiento. Los miembros de una clase incluyen todos los miembros declarados en la clase, junto con todos los miembros (excepto constructores y finalizadores) declarados en todas las clases de su jerarquía de herencia. Los miembros privados de clases base se heredan en las clases derivadas, pero estas no pueden tener acceso a ellos.  
  
 En la tabla siguiente se enumeran los tipos de miembros que puede contener una clase o struct:  
  
|Miembro|DESCRIPCIÓN|  
|------------|-----------------|  
|[Campos](../../../csharp/programming-guide/classes-and-structs/fields.md)|Los campos son variables declaradas en el ámbito de clase. Un campo puede ser un tipo numérico integrado o una instancia de otra clase. Por ejemplo, una clase de calendario puede tener un campo con la fecha actual.|  
|[Constantes](../../../csharp/programming-guide/classes-and-structs/constants.md)|Las constantes son campos cuyo valor se establece en tiempo de compilación y no se puede cambiar.|  
|[Propiedades](../../../csharp/programming-guide/classes-and-structs/properties.md)|Las propiedades son métodos de una clase a los que se obtiene acceso como si fueran campos de esa clase. Una propiedad puede proporcionar protección a un campo de clase con el fin de evitar que se cambie sin el conocimiento del objeto.|  
|[Métodos](../../../csharp/programming-guide/classes-and-structs/methods.md)|Los métodos definen las acciones que una clase puede realizar. Los métodos pueden aceptar parámetros que proporcionan datos de entrada y devolver datos de salida a través de parámetros. Los métodos también pueden devolver un valor directamente, sin usar ningún parámetro.|  
|[Eventos](../../../csharp/programming-guide/events/index.md)|Los eventos proporcionan a otros objetos notificaciones sobre lo que ocurre, como clics en botones o la realización correcta de un método. Los eventos se definen y desencadenan mediante delegados.|  
|[Operadores](../../../csharp/programming-guide/statements-expressions-operators/operators.md)|Los operadores sobrecargados se consideran miembros de tipo. Si se sobrecarga un operador, se define como método estático público en un tipo. Para obtener más información, vea [Sobrecarga de operadores](../../../csharp/language-reference/operators/operator-overloading.md).|  
|[Indizadores](../../../csharp/programming-guide/indexers/index.md)|Los indizadores permiten indizar un objeto de manera similar a como se hace con las matrices.|  
|[Constructores](../../../csharp/programming-guide/classes-and-structs/constructors.md)|Los constructores son métodos a los que se llama cuando el objeto se crea por primera vez. Se usan a menudo para inicializar los datos de un objeto.|  
|[Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)|En C#, los finalizadores se usan en raras ocasiones. Son métodos a los que llama el motor de ejecución del runtime cuando el objeto está a punto de quitarse de la memoria. Generalmente se utilizan para asegurarse de que los recursos que se deben liberar se controlan apropiadamente.|  
|[Tipos anidados](../../../csharp/programming-guide/classes-and-structs/nested-types.md)|Los tipos anidados son tipos declarados dentro de otro tipo. Los tipos anidados se usan a menudo para describir objetos utilizados únicamente por los tipos que los contienen.|  
  
## <a name="see-also"></a>Vea también

- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Clases](../../../csharp/programming-guide/classes-and-structs/classes.md)
- [Métodos](../../../csharp/programming-guide/classes-and-structs/methods.md)
- [Constructores](../../../csharp/programming-guide/classes-and-structs/constructors.md)
- [Finalizadores](../../../csharp/programming-guide/classes-and-structs/destructors.md)
- [Propiedades](../../../csharp/programming-guide/classes-and-structs/properties.md)
- [Campos](../../../csharp/programming-guide/classes-and-structs/fields.md)
- [Indizadores](../../../csharp/programming-guide/indexers/index.md)
- [Eventos](../../../csharp/programming-guide/events/index.md)
- [Tipos anidados](../../../csharp/programming-guide/classes-and-structs/nested-types.md)
- [Operadores](../../../csharp/programming-guide/statements-expressions-operators/operators.md)
