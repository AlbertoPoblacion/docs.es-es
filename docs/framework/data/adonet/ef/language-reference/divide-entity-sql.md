---
title: '- (Dividir) (Entity SQL)'
ms.date: 03/30/2017
ms.assetid: ef48c368-f3ed-4275-8ada-4e9649781262
ms.openlocfilehash: ca63835a3be23137a1a40d6d6597083ae2128ac7
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59094897"
---
# <a name="-divide-entity-sql"></a>/ (Dividir) (Entity SQL)
Divide un número entre otro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
dividend / divisor  
```  
  
## <a name="arguments"></a>Argumentos  
 `dividend`  
 Expresión numérica que se va a dividir. `dividend` es cualquier expresión válida de cualquiera de los tipos de datos numéricos.  
  
 `divisor`  
 Expresión numérica entre la que se divide el dividendo. `divisor` es cualquier expresión válida de cualquiera de los tipos de datos numéricos.  
  
## <a name="result-types"></a>Tipos de resultado  
 El tipo de datos que resulta de la promoción de tipos implícita de dos argumentos. Para obtener más información acerca de la promoción de tipos implícita, vea [Type System](../../../../../../docs/framework/data/adonet/ef/language-reference/type-system-entity-sql.md).  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta de Entity SQL usa el aritmético / operador para dividir un número por otro. La consulta se basa en el modelo AdventureWorks Sales. Para compilar y ejecutar esta consulta, siga estos pasos:  
  
1.  Siga el procedimiento de [Cómo: Ejecutar una consulta que devuelve resultados StructuralType](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md).  
  
2.  Pase la consulta siguiente como argumento al método `ExecuteStructuralTypeQuery` :  
  
 [!code-csharp[DP EntityServices Concepts 2#DIVIDE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#divide)]  
  
## <a name="see-also"></a>Vea también

- [Referencia de Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
