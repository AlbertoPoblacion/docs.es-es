---
title: 'Solución del problema: Agentes de escucha de registro (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- event logs, troubleshooting
- troubleshooting Visual Basic, event logs
- troubleshooting event logs
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
ms.openlocfilehash: f1201262fd09145679a9f70cd742294d248fedb3
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58831701"
---
# <a name="troubleshooting-log-listeners-visual-basic"></a>Solución del problema: Agentes de escucha de registro (Visual Basic)
Puede usar los objetos `My.Application.Log` y `My.Log` para registrar información sobre los eventos que se producen en su aplicación.  
  
 Para determinar qué agentes de escucha de registro reciben esos mensajes, vea [Tutorial: Determinar el lugar en el que My.Application.Log escribe la información](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md).  
  
 El objeto `Log` puede usar el filtrado del registro para limitar la cantidad de información que registra. Si los filtros se configuran de manera incorrecta, los registros pueden contener información equivocada. Para más información sobre el filtrado, vea [Tutorial: Filtrar el resultado de My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md).  
  
 En cambio, si un registro se configura incorrectamente, puede necesitar más información sobre su configuración actual. Puede obtener esta información mediante la propiedad `TraceSource` avanzada del registro.  
  
### <a name="to-determine-the-log-listeners-for-the-log-object-in-code"></a>Para determinar los agentes de escucha de registro del objeto Log con código  
  
1.  Importe el espacio de nombres <xref:System.Diagnostics> al principio del archivo de código. Para obtener más información, consulte [Instrucción Imports (Tipo y espacio de nombres de .NET)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
     [!code-vb[VbVbalrMyApplicationLog#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#13)]  
  
2.  Cree una función que devuelva una cadena compuesta por información de cada uno de los agentes de escucha del registro.  
  
     [!code-vb[VbVbalrMyApplicationLog#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#14)]  
  
3.  Pase la colección de los agentes de escucha de seguimiento del registro a la función `GetListeners` y muestre el valor devuelto.  
  
     [!code-vb[VbVbalrMyApplicationLog#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#19)]  
  
     Para obtener más información, vea <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A>.  
  
## <a name="see-also"></a>Vea también

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- [Trabajar con registros de aplicaciones](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [Tutorial: Determinar el lugar en el que My.Application.Log escribe la información](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
