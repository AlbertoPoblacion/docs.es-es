---
title: Filtrar para agregar instrucciones de seguimiento al código de una aplicación
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tracing [.NET Framework], conditional writes based on switches
- trace statements
- WriteLineIf method
- tracing [.NET Framework], adding trace statements
- Assert method, tracing code
- trace switches, conditional writes based on switches
- WriteIf method
ms.assetid: f3a93fa7-1717-467d-aaff-393e5c9828b4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b39646655c175497533aa6dc358c6966acc27344
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59325597"
---
# <a name="how-to-add-trace-statements-to-application-code"></a>Filtrar para agregar instrucciones de seguimiento al código de una aplicación
Los métodos que se usan con mayor frecuencia para traza son los métodos para escribir los resultados en agentes de escucha: **Escribir**, **WriteIf**, **WriteLine**, **WriteLineIf**, **Assert**, y **producirá un error en**. Estos métodos pueden dividirse en dos categorías: **Escribir**, **WriteLine**, y **producirá un error en** emiten resultados de forma incondicional, mientras que **WriteIf**, **WriteLineIf**y  **Assert** comprueban una condición booleana y escriben o no escriben en función del valor de la condición. **WriteIf** y **WriteLineIf** emiten resultados si la condición es `true` y **Assert** emite resultados si la condición es `false`.  
  
 Al diseñar la estrategia de depuración y traza, debe pensar cómo desea presentar los resultados. Varias instrucciones **Write** con información no relacionada crearán un registro difícil de leer. Por otro lado, usar **WriteLine** para colocar instrucciones relacionadas en líneas independientes puede hacer que sea difícil distinguir la información del mismo tipo. En general, use varias instrucciones **Write** cuando quiera combinar información de varios orígenes para crear un único mensaje informativo y use la instrucción **WriteLine** cuando quiera crear un único mensaje completo.  
  
### <a name="to-write-a-complete-line"></a>Para escribir una línea completa  
  
1. Llame al método <xref:System.Diagnostics.Trace.WriteLine%2A> o <xref:System.Diagnostics.Trace.WriteLineIf%2A>.  
  
     Se agrega un retorno de carro al final del mensaje que devuelve este método, para que el siguiente mensaje devuelto por **Write**, **WriteIf**, **WriteLine** o **WriteLineIf** comience en la línea siguiente:  
  
    ```vb  
    Dim errorFlag As Boolean = False  
    Trace.WriteLine("Error in AppendData procedure.")  
    Trace.WriteLineIf(errorFlag, "Error in AppendData procedure.")  
    ```  
  
    ```csharp  
    bool errorFlag = false;  
    System.Diagnostics.Trace.WriteLine ("Error in AppendData procedure.");  
    System.Diagnostics.Trace.WriteLineIf(errorFlag,   
       "Error in AppendData procedure.");  
    ```  
  
### <a name="to-write-a-partial-line"></a>Para escribir una línea parcial  
  
1. Llame al método <xref:System.Diagnostics.Trace.Write%2A> o <xref:System.Diagnostics.Trace.WriteIf%2A>.  
  
     El siguiente mensaje generado por **Write**, **WriteIf**, **WriteLine** o **WriteLineIf** empezará en la misma línea que el mensaje generado por la instrucción **Write** o **WriteIf**:  
  
    ```vb  
    Dim errorFlag As Boolean = False  
    Trace.WriteIf(errorFlag, "Error in AppendData procedure.")  
    Debug.WriteIf(errorFlag, "Transaction abandoned.")  
    Trace.Write("Invalid value for data request")  
    ```  
  
    ```csharp  
    bool errorFlag = false;  
    System.Diagnostics.Trace.WriteIf(errorFlag,   
       "Error in AppendData procedure.");  
    System.Diagnostics.Debug.WriteIf(errorFlag, "Transaction abandoned.");  
    Trace.Write("Invalid value for data request");  
    ```  
  
### <a name="to-verify-that-certain-conditions-exist-either-before-or-after-you-execute-a-method"></a>Para comprobar que se cumplen ciertas condiciones antes o después de ejecutar un método  
  
1. Llame al método <xref:System.Diagnostics.Trace.Assert%2A>.  
  
    ```vb  
    Dim i As Integer = 4  
    Trace.Assert(i = 5, "i is not equal to 5.")  
    ```  
  
    ```csharp  
    int i = 4;  
    System.Diagnostics.Trace.Assert(i == 5, "i is not equal to 5.");  
    ```  
  
    > [!NOTE]
    >  Puede usar **Assert** con la depuración y el seguimiento. En este ejemplo se envía la pila de llamadas a cualquier agente de escucha de la colección **Listeners**. Para más información, vea [Aserciones en el código administrado](/visualstudio/debugger/assertions-in-managed-code) y <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Diagnostics.Debug.WriteIf%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.Debug.WriteLineIf%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.Trace.WriteIf%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.Trace.WriteLineIf%2A?displayProperty=nameWithType>
- [Seguimiento e instrumentación de aplicaciones](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)
- [Filtrar para crear, inicializar y configurar modificadores de seguimiento](../../../docs/framework/debug-trace-profile/how-to-create-initialize-and-configure-trace-switches.md)
- [Modificadores de seguimiento](../../../docs/framework/debug-trace-profile/trace-switches.md)
- [Agentes de escucha de seguimiento](../../../docs/framework/debug-trace-profile/trace-listeners.md)
