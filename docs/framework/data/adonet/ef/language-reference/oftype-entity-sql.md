---
title: OFTYPE (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 6d259ca7-bbf0-40f8-a154-181d25c0d67e
ms.openlocfilehash: bbc3ffd4902fe8c1c41aebe88317d0e3c32f7771
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61760368"
---
# <a name="oftype-entity-sql"></a>OFTYPE (Entity SQL)
Devuelve una colección de objetos de una expresión de consulta de un tipo específico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
OFTYPE ( expression, [ONLY] test_type )  
```  
  
## <a name="arguments"></a>Argumentos  
 `expression`  
 Expresión de consulta válida que devuelve una colección de objetos.  
  
 `test_type`  
 Tipo con el que probar cada objeto que devuelve `expression` . El tipo debe estar calificado por un espacio de nombres.  
  
## <a name="return-value"></a>Valor devuelto  
 Colección de objetos que son del tipo `test_type`o de un tipo base o derivado de `test_type`. Si se especifica ONLY, solo se devolverán las instancias de `test_type` o una colección vacía.  
  
## <a name="remarks"></a>Comentarios  
 Una expresión `OFTYPE` especifica una expresión de un tipo que se emite para realizar una prueba del tipo con cada elemento de una colección.  La expresión `OFTYPE` produce una nueva colección del tipo especificado que contiene solo los elementos que eran equivalentes a ese tipo o a alguno de sus subtipos.  
  
 Una expresión `OFTYPE` es una abreviatura de la expresión de consulta siguiente:  
  
```  
select value treat(t as T) from ts as t where t is of (T)  
```  
  
 Dado que Manager es un subtipo de Employee, la expresión siguiente produce una colección de jefes (managers) únicamente a partir de una colección de empleados (employees):  
  
```  
OfType(employees, NamespaceName.Manager)  
```  
  
 También es posible convertir una colección utilizando el filtro de tipo:  
  
```  
OfType(executives, NamespaceName.Manager)  
```  
  
 Puesto que todos los ejecutivos (executive) son jefes (managers), la colección resultante todavía contiene a todos los ejecutivos originales, aunque ahora tengan el tipo de una colección de administradores.  
  
 En la tabla siguiente se muestra el comportamiento del operador `OFTYPE` en algunos patrones. Todas las excepciones se producen en el cliente antes de que se llame al proveedor:  
  
|Modelo|Comportamiento|  
|-------------|--------------|  
|OFTYPE(Collection(EntityType), EntityType)|Collection(EntityType)|  
|OFTYPE(Collection(ComplexType), ComplexType)|Produce|  
|OFTYPE(Collection(RowType), RowType)|Produce|  
  
## <a name="example"></a>Ejemplo  
 La siguiente consulta de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usa el operador OFTYPE para devolver una colección de objetos OnsiteCourse a partir de una colección de objetos Course. La consulta se basa en el [modelo School](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)).  
  
 [!code-csharp[DP EntityServices Concepts 2#OFTYPE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#oftype)]  
  
## <a name="see-also"></a>Vea también

- [Referencia de Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)
