---
title: Destrucción de subprocesos
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- destroying threads
- threading [.NET Framework], destroying threads
ms.assetid: df54e648-c5d1-47c9-bd29-8e4438c1db6d
ms.openlocfilehash: 1852135e9b7f48d6556e27f16819ddd48805af21
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73138094"
---
# <a name="destroying-threads"></a>Destrucción de subprocesos
El método <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> se utiliza para detener un subproceso administrado de forma permanente. Cuando se llama a <xref:System.Threading.Thread.Abort%2A>, Common Language Runtime produce una clase <xref:System.Threading.ThreadAbortException> en el subproceso de destino, que este último puede detectar. Para más información, consulte <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>.  
  
> [!NOTE]
> Si un subproceso ejecuta código no administrado al llamar a su método <xref:System.Threading.Thread.Abort%2A>, el tiempo de ejecución lo marca como <xref:System.Threading.ThreadState.AbortRequested?displayProperty=nameWithType>. La excepción se produce cuando el subproceso vuelve al código administrado.  
  
 Una vez que se anula un subproceso, no se puede reiniciar.  
  
 El método <xref:System.Threading.Thread.Abort%2A> no hace que el subproceso se anule inmediatamente, porque el subproceso de destino puede detectar <xref:System.Threading.ThreadAbortException> y ejecutar cantidades arbitrarias de código en un bloque `finally`. Puede llamar a <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> si tiene que esperar hasta que haya finalizado el subproceso. <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> es una llamada de bloqueo que no realiza ninguna devolución hasta que el subproceso se haya dejado de ejecutar realmente o hasta que haya transcurrido un intervalo de tiempo de espera opcional. El subproceso anulado podría llamar al método <xref:System.Threading.Thread.ResetAbort%2A> o llevar a cabo el procesamiento sin enlazar en un bloqueo `finally`, por lo que si no especifica un tiempo de espera, no se garantiza que la espera finalice.  
  
 Los subprocesos que esperan una llamada al método <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType> pueden interrumpirse con otros subprocesos que llaman a <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType>.  
  
## <a name="handling-threadabortexception"></a>Control de ThreadAbortException  
 Si espera que se anule el subproceso, como resultado de una llamada a <xref:System.Threading.Thread.Abort%2A> desde su propio código o como resultado de la descarga de un dominio de aplicación en que se ejecuta el subproceso (<xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> usa <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> para terminar los subprocesos), el subproceso debe controlar <xref:System.Threading.ThreadAbortException> y realizar cualquier procesamiento final en una cláusula `finally`, como se muestra en el código siguiente.  
  
```vb  
Try  
    ' Code that is executing when the thread is aborted.  
Catch ex As ThreadAbortException  
    ' Clean-up code can go here.  
    ' If there is no Finally clause, ThreadAbortException is  
    ' re-thrown by the system at the end of the Catch clause.   
Finally  
    ' Clean-up code can go here.  
End Try  
' Do not put clean-up code here, because the exception   
' is rethrown at the end of the Finally clause.  
```  
  
```csharp  
try   
{  
    // Code that is executing when the thread is aborted.  
}   
catch (ThreadAbortException ex)   
{  
    // Clean-up code can go here.  
    // If there is no Finally clause, ThreadAbortException is  
    // re-thrown by the system at the end of the Catch clause.   
}  
// Do not put clean-up code here, because the exception   
// is rethrown at the end of the Finally clause.  
```  
  
 El código de limpieza debe estar en la cláusula `catch` o en la cláusula `finally`, porque el sistema vuelve a generar <xref:System.Threading.ThreadAbortException> al final de la cláusula `finally` o al final de la cláusula `catch` si no existe la cláusula `finally`.  
  
 Puede impedir que el sistema vuelva a generar la excepción mediante una llamada al método <xref:System.Threading.Thread.ResetAbort%2A?displayProperty=nameWithType>. Sin embargo, debe hacerlo solo si su propio código generó <xref:System.Threading.ThreadAbortException>.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Threading.ThreadAbortException>
- <xref:System.Threading.Thread>
- [Usar subprocesos y subprocesamiento](../../../docs/standard/threading/using-threads-and-threading.md)
