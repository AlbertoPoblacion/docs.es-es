---
title: Filtrar para crear e inicializar agentes de escucha de seguimiento
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- initializing trace listeners
- trace listeners, creating
- trace listeners, initializing
- tracing [.NET Framework], trace listeners
- logs, trace listeners
ms.assetid: 21726de1-61ee-4fdc-9dd0-3be49324d066
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 85cf8f32a3dbf283e75052548f5963e8a7da0ed2
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59321060"
---
# <a name="how-to-create-and-initialize-trace-listeners"></a>Filtrar para crear e inicializar agentes de escucha de seguimiento
Las clases <xref:System.Diagnostics.Debug?displayProperty=nameWithType> y <xref:System.Diagnostics.Trace?displayProperty=nameWithType> envían mensajes a objetos denominados agentes de escucha que reciben y procesan estos mensajes. Un agente de escucha de este tipo, <xref:System.Diagnostics.DefaultTraceListener?displayProperty=nameWithType>, se crea y se inicializa automáticamente si la traza o la depuración está habilitada. Si desea que los resultados de <xref:System.Diagnostics.Trace> o <xref:System.Diagnostics.Debug> se envíen a otros destinos adicionales, deberá crear e inicializar agentes de escucha adicionales.  
  
 Los agentes de escucha que cree deben reflejar las necesidades de la aplicación. Por ejemplo, si desea un registro de texto de todo el resultado de traza, cree un agente de escucha <xref:System.Diagnostics.TextWriterTraceListener>, que escribe todo el resultado en un nuevo archivo de texto cuando se habilita. Por otra parte, si desea ver el resultado solo durante la ejecución de la aplicación, cree un agente de escucha <xref:System.Diagnostics.ConsoleTraceListener>, que envía todo el resultado a una ventana de consola. <xref:System.Diagnostics.EventLogTraceListener> puede dirigir el resultado de traza a un registro de eventos. Para más información, vea [Agentes de escucha de seguimiento](../../../docs/framework/debug-trace-profile/trace-listeners.md).  
  
 Puede crear agentes de escucha de seguimiento en un [archivo de configuración de la aplicación](../../../docs/framework/configure-apps/index.md) o en el código. Se recomienda el uso de archivos de configuración de la aplicación, ya que permiten agregar, modificar o quitar agentes de escucha de traza sin necesidad de modificar el código.  
  
### <a name="to-create-and-use-a-trace-listener-by-using-a-configuration-file"></a>Para crear y usar un agente de escucha de traza mediante un archivo de configuración  
  
1. Declare el agente de escucha de traza en el archivo de configuración de la aplicación. Si el agente de escucha que va a crear requiere otros objetos, declárelos también. En el ejemplo siguiente, se muestra cómo crear un agente de escucha denominado `myListener` que escribe en el archivo de texto `TextWriterOutput.log`.  
  
    ```xml  
    <configuration>  
      <system.diagnostics>  
        <trace autoflush="false" indentsize="4">  
          <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="TextWriterOutput.log" />  
            <remove name="Default" />  
          </listeners>  
        </trace>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
2. Utilice la clase <xref:System.Diagnostics.Trace> en el código para escribir un mensaje a los agentes de escucha de traza.   
  
    ```vb  
    Trace.TraceInformation("Test message.")  
    ' You must close or flush the trace to empty the output buffer.  
    Trace.Flush()  
    ```  
  
    ```csharp  
    Trace.TraceInformation("Test message.");  
    // You must close or flush the trace to empty the output buffer.  
    Trace.Flush();  
    ```  
  
### <a name="to-create-and-use-a-trace-listener-in-code"></a>Crear y utilizar un agente de escucha de traza en el código  
  
-   Agregue el agente de escucha de traza a la colección <xref:System.Diagnostics.Trace.Listeners%2A> y envíe información de traza a los agentes de escucha.  
  
    ```vb  
    Trace.Listeners.Add(New TextWriterTraceListener("TextWriterOutput.log", "myListener"))  
    Trace.TraceInformation("Test message.")  
    ' You must close or flush the trace to empty the output buffer.  
    Trace.Flush()  
    ```  
  
    ```csharp  
    Trace.Listeners.Add(new TextWriterTraceListener("TextWriterOutput.log", "myListener"));  
    Trace.TraceInformation("Test message.");  
    // You must close or flush the trace to empty the output buffer.  
    Trace.Flush();  
    ```  
  
     - O  
  
-   Si no desea que el agente de escucha reciba el resultado de la traza, no lo agregue a la colección <xref:System.Diagnostics.Trace.Listeners%2A>. Puede emitir la salida a través de un agente de escucha independientemente de la colección <xref:System.Diagnostics.Trace.Listeners%2A>, llamando a los propios métodos de salida del agente de escucha. El siguiente ejemplo muestra cómo escribir una línea a un agente de escucha que no se encuentra en la colección <xref:System.Diagnostics.Trace.Listeners%2A>:   
  
    ```vb  
    Dim myListener As New TextWriterTraceListener("TextWriterOutput.log", "myListener")  
    myListener.WriteLine("Test message.")  
    ' You must close or flush the trace listener to empty the output buffer.  
    myListener.Flush()  
    ```  
  
    ```csharp  
    TextWriterTraceListener myListener = new TextWriterTraceListener("TextWriterOutput.log", "myListener");  
    myListener.WriteLine("Test message.");  
    // You must close or flush the trace listener to empty the output buffer.  
    myListener.Flush();  
    ```  
  
## <a name="see-also"></a>Vea también

- [Agentes de escucha de seguimiento](../../../docs/framework/debug-trace-profile/trace-listeners.md)
- [Modificadores de seguimiento](../../../docs/framework/debug-trace-profile/trace-switches.md)
- [Filtrar para agregar instrucciones de seguimiento al código de una aplicación](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)
- [Seguimiento e instrumentación de aplicaciones](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)
