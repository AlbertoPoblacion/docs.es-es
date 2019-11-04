---
title: Agrupar datos (C#)
ms.date: 07/20/2015
ms.assetid: e414e9e4-343a-4e6e-858f-4a30c5e64492
ms.openlocfilehash: e7f10b121a7a1c599d88731a806fe784eb1a7e66
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/01/2019
ms.locfileid: "73423418"
---
# <a name="grouping-data-c"></a>Agrupar datos (C#)
El agrupamiento hace referencia a la operación de colocar los datos en grupos de manera que los elementos de cada grupo compartan un atributo común.  
  
 La ilustración siguiente muestra los resultados de agrupar una secuencia de caracteres. La clave de cada grupo es el carácter.  
  
 ![Diagrama que muestra una operación de agrupación de LINQ.](./media/grouping-data/linq-group-operation.png)  
  
 Los métodos de operador de consulta estándar que agrupan elementos de datos se enumeran en la sección siguiente.  
  
## <a name="methods"></a>Métodos  
  
|Nombre del método|DESCRIPCIÓN|Sintaxis de la expresión de consulta de C#|Más información|  
|-----------------|-----------------|---------------------------------|----------------------|  
|GroupBy|Agrupa los elementos que comparten un atributo común. Cada grupo se representa mediante un objeto <xref:System.Linq.IGrouping%602>.|`group … by`<br /><br /> O bien<br /><br /> `group … by … into …`|<xref:System.Linq.Enumerable.GroupBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupBy%2A?displayProperty=nameWithType>|  
|ToLookup|Inserta elementos a una <xref:System.Linq.Lookup%602> (un diccionario uno a varios) basándose en una función de selector de claves.|No es aplicable.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>Ejemplo de sintaxis de expresiones de consulta  
 El ejemplo de código siguiente usa la cláusula `group by` para agrupar los enteros de una lista según sean pares o impares.  
  
```csharp  
List<int> numbers = new List<int>() { 35, 44, 200, 84, 3987, 4, 199, 329, 446, 208 };  
  
IEnumerable<IGrouping<int, int>> query = from number in numbers  
                                         group number by number % 2;  
  
foreach (var group in query)  
{  
    Console.WriteLine(group.Key == 0 ? "\nEven numbers:" : "\nOdd numbers:");  
    foreach (int i in group)  
        Console.WriteLine(i);  
}  
  
/* This code produces the following output:  
  
    Odd numbers:  
    35  
    3987  
    199  
    329  
  
    Even numbers:  
    44  
    200  
    84  
    4  
    446  
    208  
*/  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Linq>
- [Standard Query Operators Overview (C#)](./standard-query-operators-overview.md) (Información general sobre operadores de consulta estándar (C#))
- [group (cláusula)](../../../language-reference/keywords/group-clause.md)
- [Cómo: Crear un grupo anidado](../../../linq/create-a-nested-group.md)
- [Cómo: Agrupar archivos por extensión (LINQ) (C#)](./how-to-group-files-by-extension-linq.md)
- [Cómo: Agrupar los resultados de consultas](../../../linq/group-query-results.md)
- [Cómo: Realizar una subconsulta en una operación de agrupación](../../../linq/perform-a-subquery-on-a-grouping-operation.md)
- [Cómo: Dividir un archivo en varios mediante el uso de grupos (LINQ) (C#)](./how-to-split-a-file-into-many-files-by-using-groups-linq.md)
