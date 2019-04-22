---
title: Distinct (Cláusula, Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryDistinct
helpviewer_keywords:
- Distinct clause [Visual Basic]
- Distinct statement [Visual Basic]
- queries [Visual Basic], Distinct
ms.assetid: 86f42614-0d8f-4ffc-b888-ce8a37a8d36a
ms.openlocfilehash: fbca9fa8aa227d8d5b6488bef179f4bda08bb38c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58830063"
---
# <a name="distinct-clause-visual-basic"></a>Distinct (Cláusula, Visual Basic)
Restringe los valores de la variable de rango actual para eliminar valores duplicados en las cláusulas de consulta subsiguientes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
Distinct  
```  
  
## <a name="remarks"></a>Comentarios  
 Puede usar el `Distinct` cláusula para devolver una lista de elementos únicos. El `Distinct` cláusula hace que la consulta pasar por alto los resultados de consulta duplicada. El `Distinct` cláusula se aplica a valores duplicados para todos los devueltos campos especificados por el `Select` cláusula. Si no hay ningún `Select` cláusula se especifica, el `Distinct` cláusula se aplica a la variable de rango para la consulta identificada en el `From` cláusula. Si la variable de rango no es un tipo inmutable, la consulta omitirá únicamente un resultado de consulta si todos los miembros del tipo coinciden con un resultado de consulta existente.  
  
## <a name="example"></a>Ejemplo  
 La expresión de consulta siguiente combina una lista de clientes y una lista de pedidos del cliente. El `Distinct` cláusula se incluye para devolver una lista de nombres de cliente únicos y ordenar las fechas.  
  
 [!code-vb[VbSimpleQuerySamples#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#20)]  
  
## <a name="see-also"></a>Vea también

- [Introducción a LINQ en Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [Consultas](../../../visual-basic/language-reference/queries/index.md)
- [From (cláusula)](../../../visual-basic/language-reference/queries/from-clause.md)
- [Select (cláusula)](../../../visual-basic/language-reference/queries/select-clause.md)
- [Where (cláusula)](../../../visual-basic/language-reference/queries/where-clause.md)
