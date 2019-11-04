---
title: Procedimiento para recorrer un árbol binario con tareas en paralelo
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, how to traverse a tree
ms.assetid: 4265d169-6c69-4f36-b10d-b7ae7f72f4df
ms.openlocfilehash: b79337e6ee8057506ff87c696cecd6b038eeebfc
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73141648"
---
# <a name="how-to-traverse-a-binary-tree-with-parallel-tasks"></a>Procedimiento para recorrer un árbol binario con tareas en paralelo
En el ejemplo siguiente se muestran dos formas de usar las tareas paralelas para recorrer una estructura de datos en árbol. La creación del árbol se deja como un ejercicio.  
  
## <a name="example"></a>Ejemplo  
 [!code-csharp[TPL#16](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl/cs/tpl.cs#16)]
 [!code-vb[TPL#16](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl/vb/treewalk.vb#16)]  
  
 Los dos métodos que se muestran son funcionalmente equivalentes. Con el uso del método <xref:System.Threading.Tasks.TaskFactory.StartNew%2A> para crear y ejecutar las tareas, estas devuelven un identificador que puede usarse para esperar las tareas y controlar excepciones.  
  
## <a name="see-also"></a>Vea también

- [Biblioteca TPL](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)
