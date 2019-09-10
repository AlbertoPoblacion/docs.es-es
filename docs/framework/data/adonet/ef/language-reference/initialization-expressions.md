---
title: Expresiones de inicialización
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 98daef1f-15d4-483e-985c-d78ea3abe8c8
ms.openlocfilehash: 5d6656ab77f7ad0f7366a230d98b95cff5b2677b
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854434"
---
# <a name="initialization-expressions"></a>Expresiones de inicialización
Una expresión de inicialización inicializa un objeto nuevo. Se admiten la mayoría de las expresiones de inicialización, incluso las de Visual Basic 9.0 y C# 3.0. Los tipos siguientes pueden ser inicializados y devueltos por una consulta de LINQ to Entities:  
  
- Una colección de cero o más objetos entidad con tipo o una proyección de tipos complejos definidos en el modelo conceptual.  
  
- Tipos CLR admitidos por el Entity Framework.
  
- Colecciones insertadas.  
  
- Tipos anónimos.  
  
 En el ejemplo siguiente se muestra la inicialización de tipos anónimos en sintaxis de expresiones de consulta:  
  
 [!code-csharp[DP L2E Conceptual Examples#AnonymousTypeInitialization](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#anonymoustypeinitialization)]
 [!code-vb[DP L2E Conceptual Examples#AnonymousTypeInitialization](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#anonymoustypeinitialization)]  
  
 El ejemplo siguiente de sintaxis de la consulta basada en métodos muestra la inicialización de los tipos anónimos:  
  
 [!code-csharp[DP L2E Conceptual Examples#AnonymousTypeInitialization_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#anonymoustypeinitialization_mq)]
 [!code-vb[DP L2E Conceptual Examples#AnonymousTypeInitialization_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#anonymoustypeinitialization_mq)]  
  
 También se admite la inicialización de clases definidas por el usuario. Se admite el patrón de inicialización de C# 3.0 y Visual Basic 9.0, y se supone que el captador y el establecedor de la propiedad son simétricos. El ejemplo siguiente de la sintaxis de las expresiones de consulta muestra una clase personalizada que se inicializa en la consulta:  
  
 [!code-csharp[DP L2E Conceptual Examples#MyOrder](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#myorder)]
 [!code-vb[DP L2E Conceptual Examples#MyOrder](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#myorder)]  
  
 [!code-csharp[DP L2E Conceptual Examples#TypeInitialization](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#typeinitialization)]
 [!code-vb[DP L2E Conceptual Examples#TypeInitialization](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#typeinitialization)]  
  
 El ejemplo siguiente de la sintaxis de las consultas basadas en métodos muestra una clase personalizada que se inicializa en la consulta:  
  
 [!code-csharp[DP L2E Conceptual Examples#TypeInitialization_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#typeinitialization_mq)]
 [!code-vb[DP L2E Conceptual Examples#TypeInitialization_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#typeinitialization_mq)]  
  
## <a name="see-also"></a>Vea también

- [Expresiones en consultas de LINQ to Entities](expressions-in-linq-to-entities-queries.md)
