---
title: Programación asincrónica con Async y Await (Visual Basic)
ms.date: 07/20/2015
ms.assetid: bd7e462b-583b-4395-9c36-45aa9e61072c
---
# <a name="asynchronous-programming-with-async-and-await-visual-basic"></a>Programación asincrónica con Async y Await (Visual Basic)
Puede evitar cuellos de botella de rendimiento y mejorar la capacidad de respuesta total de la aplicación mediante la programación asincrónica. Sin embargo, las técnicas tradicionales para escribir aplicaciones asincrónicas pueden resultar complicadas, haciéndolas difícil de escribir, depurar y mantener.  
  
 Visual Studio 2012 introdujo un enfoque simplificado, la programación asincrónica, que aprovecha la compatibilidad asincrónica de .NET Framework 4.5 y versiones posteriores, así como de Windows Runtime. El compilador realiza el trabajo difícil que el desarrollador suele realizar y la aplicación conserva una estructura lógica similar al código sincrónico. Como resultado, se obtienen todas las ventajas de la programación asincrónica con una parte del trabajo.  
  
 Este tema proporciona información general sobre cuándo y cómo utilizar la programación asincrónica e incluye vínculos que admiten temas con detalles y ejemplos.  
  
## <a name="BKMK_WhentoUseAsynchrony"></a> La asincronía mejora la capacidad de respuesta  
 La asincronía es esencial para actividades que pueden producir bloqueos, por ejemplo cuando la aplicación obtiene acceso a Internet. Tener acceso a un recurso web a veces es lento o va retrasado. Si tal actividad queda bloqueada dentro de un proceso sincrónico, toda la aplicación deberá esperar. En un proceso asincrónico, la aplicación puede continuar con otro trabajo que no dependa del recurso web hasta que finaliza la tarea que puede producir bloqueos.  
  
 En la tabla siguiente se muestran las áreas típicas donde la programación asincrónica mejora su capacidad de respuesta. Las API enumeradas desde .NET Framework 4.5 y Windows Runtime contienen métodos que admiten la programación asincrónica.  
  
|Área de aplicación|Compatibilidad de las API que contienen métodos asincrónicos|  
|----------------------|------------------------------------------------|  
|Acceso web|<xref:System.Net.Http.HttpClient>, <xref:Windows.Web.Syndication.SyndicationClient>|  
|Trabajar con archivos|<xref:Windows.Storage.StorageFile>, <xref:System.IO.StreamWriter>, <xref:System.IO.StreamReader>, <xref:System.Xml.XmlReader>|  
|Trabajar con imágenes|<xref:Windows.Media.Capture.MediaCapture>, <xref:Windows.Graphics.Imaging.BitmapEncoder>, <xref:Windows.Graphics.Imaging.BitmapDecoder>|  
|Programar WCF|[Operaciones sincrónicas y asincrónicas](../../../../framework/wcf/synchronous-and-asynchronous-operations.md)|  
|||  
  
 La asincronía es especialmente valiosa para aquellas aplicaciones que obtienen acceso al subproceso de interfaz de usuario, ya que todas las actividades relacionadas con la interfaz de usuario normalmente comparten un único subproceso. Si se bloquea un proceso en una aplicación sincrónica, se bloquean todos. La aplicación deja de responder y puede que se piense que se ha producido un error cuando en realidad la aplicación está esperando.  
  
 Cuando se usan métodos asincrónicos, la aplicación continúa respondiendo a la interfaz de usuario. Puede cambiar el tamaño o minimizar una ventana, por ejemplo, o puede cerrar la aplicación si no desea esperar a que finalice.  
  
 El enfoque basado en asincrónico agrega el equivalente de una transmisión automática a la lista de opciones entre las que puede elegir al diseñar operaciones asincrónicas. Es decir, obtiene todas las ventajas de la programación asincrónica tradicional pero con mucho menos trabajo de desarrollador.  
  
## <a name="BKMK_HowtoWriteanAsyncMethod"></a> Los métodos asincrónicos son más fáciles de escribir  
 Las palabras clave [Async](../../../../visual-basic/language-reference/modifiers/async.md) y [Await](../../../../visual-basic/language-reference/modifiers/async.md) en Visual Basic son fundamentales en la programación asincrónica. Con esas dos palabras clave, se pueden utilizar los recursos en .NET Framework o en Windows Runtime para crear un método asincrónico casi tan fácilmente como se crea un método sincrónico. Los métodos asincrónicos que se definen utilizando `Async` y `Await` se denominan métodos asincrónicos.  
  
 En el ejemplo siguiente se muestra un método asincrónico. Casi todo el código deberá ser totalmente familiar. Los comentarios informan sobre las características que se agregan para crear la asincronía.  
  
 Puede encontrar un archivo de ejemplo completo de Windows Presentation Foundation (WPF) al final de este tema y puede descargar el ejemplo de [Async Sample: Example from "Asynchronous Programming with Async and Await"](https://code.msdn.microsoft.com/Async-Sample-Example-from-9b9f505c) (Ejemplo de async: Ejemplo de "Programación asincrónica con Async y Await).  
  
```vb  
' Three things to note in the signature:  
'  - The method has an Async modifier.   
'  - The return type is Task or Task(Of T). (See "Return Types" section.)  
'    Here, it is Task(Of Integer) because the return statement returns an integer.  
'  - The method name ends in "Async."  
Async Function AccessTheWebAsync() As Task(Of Integer)  
  
    ' You need to add a reference to System.Net.Http to declare client.  
    Dim client As HttpClient = New HttpClient()  
  
    ' GetStringAsync returns a Task(Of String). That means that when you await the  
    ' task you'll get a string (urlContents).  
    Dim getStringTask As Task(Of String) = client.GetStringAsync("https://msdn.microsoft.com")  
  
    ' You can do work here that doesn't rely on the string from GetStringAsync.  
    DoIndependentWork()  
  
    ' The Await operator suspends AccessTheWebAsync.  
    '  - AccessTheWebAsync can't continue until getStringTask is complete.  
    '  - Meanwhile, control returns to the caller of AccessTheWebAsync.  
    '  - Control resumes here when getStringTask is complete.   
    '  - The Await operator then retrieves the string result from getStringTask.  
    Dim urlContents As String = Await getStringTask  
  
    ' The return statement specifies an integer result.  
    ' Any methods that are awaiting AccessTheWebAsync retrieve the length value.  
    Return urlContents.Length  
End Function  
```  
  
 Si `AccessTheWebAsync` no hay ningún trabajo que se pueda hacer entre llamar a `GetStringAsync` y esperar a su finalización, se puede simplificar el código llamando y esperando en la siguiente instrucción única.  
  
```vb  
Dim urlContents As String = Await client.GetStringAsync()  
```  
  
 Las siguientes características resumen lo que hace que el ejemplo anterior sea un método asincrónico.  
  
-   Method Signature incluye un modificador `Async`.  
  
-   El nombre de un método asincrónico, por convención, finaliza con un sufijo “Async”.  
  
-   El tipo de valor devuelto es uno de los tipos siguientes:  
  
    -   <xref:System.Threading.Tasks.Task%601> si el método tiene una instrucción return en la que el operando tiene el tipo TResult.  
  
    -   <xref:System.Threading.Tasks.Task> si el método no tiene ninguna instrucción return ni tiene una instrucción return sin operando.  
  
    -   [Sub](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md) si está escribiendo un controlador de eventos asincrónicos.  
  
     Para obtener más información, vea "Tipos de valor devuelto y parámetros" más adelante en este tema.  
  
-   El método normalmente incluye al menos una expresión await, que marca un punto en el que el método no puede continuar hasta que se completa la operación asincrónica en espera. Mientras tanto, se suspende el método y el control vuelve al llamador del método. La sección siguiente de este tema muestra lo que sucede en el punto de suspensión.  
  
 En métodos asincrónicos, se utilizan las palabras clave y los tipos proporcionados para indicar lo que se desea hacer y el compilador realiza el resto, incluido el seguimiento de qué debe ocurrir cuando el control vuelve a un punto de espera en un método suspendido. Algunos procesos de rutina, tales como bucles y control de excepciones, pueden ser difíciles de controlar en código asincrónico tradicional. En un método asincrónico, se pueden escribir estos elementos como se haría en una solución sincrónica y se resuelve este problema.  
  
 Para obtener más información sobre la asincronía en versiones anteriores de .NET Framework, vea [TPL y la programación asincrónica tradicional de .NET Framework](../../../../standard/parallel-programming/tpl-and-traditional-async-programming.md).  
  
## <a name="BKMK_WhatHappensUnderstandinganAsyncMethod"></a> Lo que ocurre en un método asincrónico  
 Lo más importante de entender en la programación asincrónica es cómo el flujo de control pasa de un método a otro. El diagrama siguiente le guía por el proceso.  
  
 ![Diagrama que muestra el seguimiento de un programa asincrónico.](./media/index/navigation-trace-async-program.png)  
  
 Los números en el diagrama se corresponden con los pasos siguientes.  
  
1.  Un controlador de eventos llama a y espera el método asincrónico `AccessTheWebAsync`.  
  
2.  `AccessTheWebAsync` crea una instancia <xref:System.Net.Http.HttpClient> y llama al método asincrónico <xref:System.Net.Http.HttpClient.GetStringAsync%2A> para descargar el contenido de un sitio web como una cadena.  
  
3.  Sucede algo en `GetStringAsync` que suspende el progreso. Quizás debe esperar a un sitio web para realizar la descarga o alguna otra actividad de bloqueo. Para evitar el bloqueo de recursos, `GetStringAsync` genera un control a su llamador, `AccessTheWebAsync`.  
  
     `GetStringAsync` devuelve <xref:System.Threading.Tasks.Task%601> donde TResult es una cadena y `AccessTheWebAsync` asigna la tarea a la variable `getStringTask`. La tarea representa el proceso actual para la llamada a `GetStringAsync`, con el compromiso de generar un valor de cadena real cuando se completa el trabajo.  
  
4.  Debido a que `getStringTask` no se ha esperado, `AccessTheWebAsync` puede continuar con otro trabajo que no dependa del resultado final de `GetStringAsync`. Ese trabajo se representa mediante una llamada al método sincrónico `DoIndependentWork`.  
  
5.  `DoIndependentWork` es un método sincrónico que funciona y vuelve al llamador.  
  
6.  `AccessTheWebAsync` se ha quedado sin el trabajo que se puede realizar sin un resultado de `getStringTask`. Después, `AccessTheWebAsync` desea calcular y devolver la longitud de la cadena descargada, pero el método no puede calcular ese valor hasta que el método tiene la cadena.  
  
     Por consiguiente, `AccessTheWebAsync` utiliza un operador await para suspender el progreso y producir el control al método que llamó `AccessTheWebAsync`. `AccessTheWebAsync` devuelve `Task<int>` (`Task(Of Integer)` en Visual Basic) al llamador. La tarea representa una sugerencia para generar un resultado entero que es la longitud de la cadena descargada.  
  
    > [!NOTE]
    >  Si se completa `GetStringAsync` (y por consiguiente `getStringTask`) antes de que `AccessTheWebAsync` lo espere, permanece el control en `AccessTheWebAsync`. El gasto de suspensión y después regresar a `AccessTheWebAsync` se desperdiciaría si el proceso denominado asincrónico (`getStringTask`) ya se ha completado y AccessTheWebSync no tiene que esperar el resultado final.  
  
     Dentro del llamador (el controlador de eventos en este ejemplo), el patrón de procesamiento continúa. El llamador puede hacer otro trabajo que no depende del resultado de `AccessTheWebAsync` antes de esperar ese resultado, o es posible que el llamador se espere inmediatamente.   El controlador de eventos está esperando `AccessTheWebAsync`, y `AccessTheWebAsync` está esperando `GetStringAsync`.  
  
7.  `GetStringAsync` completa y genera un resultado de la cadena. La llamada a `GetStringAsync` no devuelve el resultado de la cadena de la manera que cabría esperar. (Recuerde que el método ya devolvió una tarea en el paso 3). En su lugar, el resultado de la cadena se almacena en la tarea que representa la finalización del método, `getStringTask`. El operador await recupera el resultado de `getStringTask`. La instrucción de asignación asigna el resultado recuperado a `urlContents`.  
  
8.  Cuando `AccessTheWebAsync` tiene el resultado de la cadena, el método puede calcular la longitud de la cadena. El trabajo de `AccessTheWebAsync` también se completa y el controlador de eventos que espera se puede reanudar. En el ejemplo completo del final de este tema, puede comprobar que el controlador de eventos recupera e imprime el valor de resultado de longitud.  
  
 Si no está familiarizado con la programación asincrónica, reserve un minuto para ver la diferencia entre el comportamiento sincrónico y asincrónico. Un método sincrónico devuelve cuando se completa su trabajo (paso 5), pero un método asincrónico devuelve un valor de tarea cuando se suspende el trabajo (pasos 3 y 6). Cuando el método asincrónico completa finalmente el trabajo, se marca la tarea como completa y el resultado, si existe, se almacena en la tarea.  
  
 Para obtener más información sobre el flujo de control, vea [Control Flow in Async Programs (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md) (Flujo de control en programas asincrónicos [Visual Basic]).  
  
## <a name="BKMK_APIAsyncMethods"></a> Métodos asincrónicos de API  
 Tal vez se pregunte dónde encontrar métodos como `GetStringAsync` que sean compatibles con la programación asincrónica. .NET Framework 4.5 o las versiones posteriores contienen muchos miembros que trabajan con `Async` y `Await`. Puede reconocer estos miembros por el sufijo "Async" que está adjunto al nombre del miembro y por un tipo de valor devuelto <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>. Por ejemplo, la clase `System.IO.Stream` contiene métodos como <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.ReadAsync%2A> y <xref:System.IO.Stream.WriteAsync%2A> junto con los métodos sincrónicos <xref:System.IO.Stream.CopyTo%2A>, <xref:System.IO.Stream.Read%2A> y <xref:System.IO.Stream.Write%2A>.  
  
 Windows Runtime también contiene muchos métodos que puede utilizar con `Async` y `Await` en Aplicaciones Windows. Para obtener más información y ejemplos de métodos, vea [llamar a API asincrónicas en C# o Visual Basic](/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic), [programación asincrónica (aplicaciones de Windows en tiempo de ejecución)](https://docs.microsoft.com/previous-versions/windows/apps/hh464924(v=win.10)), y [WhenAny: Protocolo de puente entre .NET Framework y Windows Runtime](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/jj635140(v=vs.120)).  
  
## <a name="BKMK_Threads"></a> Subprocesos  
 La intención de los métodos Async es ser aplicaciones que no pueden producir bloqueos. Una expresión `Await` en un método asincrónico no bloquea el subproceso actual mientras la tarea esperada se encuentra en ejecución. En vez de ello, la expresión declara el resto del método como una continuación y devuelve el control al llamador del método asincrónico.  
  
 Las palabras clave `Async` y `Await` no hacen que se creen subprocesos adicionales. Los métodos Async no requieren multithreading, ya que un método asincrónico no se ejecuta en su propio subproceso. El método se ejecuta en el contexto de sincronización actual y ocupa tiempo en el subproceso únicamente cuando el método está activo. Puede utilizar <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType> para mover el trabajo enlazado a la CPU a un subproceso en segundo plano, pero un subproceso en segundo plano no ayuda con un proceso que solo está esperando a que los resultados estén disponibles.  
  
 El enfoque basado en asincrónico en la programación asincrónica es preferible a los enfoques existentes en casi todos los casos. En concreto, este enfoque es mejor que <xref:System.ComponentModel.BackgroundWorker> para operaciones dependientes de E/s porque el código es más sencillo y no tiene que proteger contra las condiciones de carrera. Junto con <xref:System.Threading.Tasks.Task.Run%2A?displayProperty=nameWithType>, la programación asincrónica es mejor que <xref:System.ComponentModel.BackgroundWorker> para las operaciones enlazadas a la CPU porque la programación asincrónica separa los detalles de coordinación en la ejecución del código del trabajo que `Task.Run` transfiere al grupo de subprocesos.  
  
## <a name="BKMK_AsyncandAwait"></a> Async y Await  
 Si especifica que un método es un método asincrónico utilizando un modificador [Async](../../../../visual-basic/language-reference/modifiers/async.md), habilita las dos funciones siguientes.  
  
-   El método asincrónico marcado puede utilizar [Await](../../../../visual-basic/language-reference/operators/await-operator.md) para designar puntos de suspensión. El operador await indica al compilador que el método asincrónico no puede continuar pasado ese punto hasta que se complete el proceso asincrónico aguardado. Mientras tanto, el control devuelve al llamador del método asincrónico.  
  
     La suspensión de un método asincrónico en una expresión `Await` no constituye una salida del método y los bloques `Finally` no se ejecutan.  
  
-   El método asincrónico marcado sí se puede esperar por los métodos que lo llaman.  
  
 Un método asincrónico normalmente contiene una o más apariciones de un operador `Await`, pero la ausencia de una expresión `Await` no causa errores de compilación. Si un método asincrónico no usa un operador `Await` para marcar el punto de suspensión, se ejecuta como un método sincrónico, a pesar del modificador `Async`. El compilador detecta una advertencia para dichos métodos.  
  
 `Async` y `Await` son palabras clave contextuales. Para mayor información y ejemplos, vea los siguientes temas:  
  
-   [Async](../../../../visual-basic/language-reference/modifiers/async.md)  
  
-   [Await (operador)](../../../../visual-basic/language-reference/operators/await-operator.md)  
  
## <a name="BKMK_ReturnTypesandParameters"></a> Tipos de valor devuelto y parámetros  
 En la programación de .NET Framework, un método asincrónico devuelve normalmente <xref:System.Threading.Tasks.Task> o <xref:System.Threading.Tasks.Task%601>. Dentro de un método asincrónico, se aplica un operador `Await` a una tarea que devuelve una llamada a otro método asincrónico.  
  
 Puede especificar <xref:System.Threading.Tasks.Task%601> como tipo de valor devuelto si el método contiene una instrucción [Return](../../../../visual-basic/language-reference/statements/return-statement.md) que especifica un operando de tipo `TResult`.  
  
 Puede utilizar `Task` como tipo de valor devuelto si el método no tiene instrucción return o tiene una instrucción return que no devuelve un operando.  
  
 En el ejemplo siguiente se muestra cómo declarar y llamar a un método que devuelve <xref:System.Threading.Tasks.Task%601> o <xref:System.Threading.Tasks.Task>.  
  
```vb  
' Signature specifies Task(Of Integer)  
Async Function TaskOfTResult_MethodAsync() As Task(Of Integer)  
  
    Dim hours As Integer  
    ' . . .  
    ' Return statement specifies an integer result.  
    Return hours  
End Function  
  
' Calls to TaskOfTResult_MethodAsync  
Dim returnedTaskTResult As Task(Of Integer) = TaskOfTResult_MethodAsync()  
Dim intResult As Integer = Await returnedTaskTResult  
' or, in a single statement  
Dim intResult As Integer = Await TaskOfTResult_MethodAsync()  
  
' Signature specifies Task  
Async Function Task_MethodAsync() As Task  
  
    ' . . .  
    ' The method has no return statement.  
End Function  
  
' Calls to Task_MethodAsync  
Task returnedTask = Task_MethodAsync()  
Await returnedTask  
' or, in a single statement  
Await Task_MethodAsync()  
```  
  
 Cada tarea devuelta representa el trabajo en curso. Una tarea encapsula la información sobre el estado del proceso asincrónico y, finalmente, el resultado final del proceso o la excepción que el proceso provoca si no tiene éxito.  
  
 Un método asincrónico también puede ser un método `Sub`. Este tipo de valor devuelto se utiliza principalmente para definir controladores de eventos, donde se requiere un tipo de valor devuelto. Los controladores de eventos asincrónicos sirven a menudo como punto de partida para programas asincrónicos.  
  
 No se puede esperar a un método asincrónico que sea un procedimiento `Sub`, y el llamador no puede capturar ninguna excepción producida por este método.  
  
 Un método aisncrónico no puede declarar ningún parámetro [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), pero el método puede llamar a los métodos que tienen estos parámetros.  
  
 Para más información y ejemplos, vea [Async Return Types (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md) (Tipos de valor devuelto asincrónicos [Visual Basic]). Para más información sobre cómo capturar excepciones en métodos asincrónicos, vea [Instrucción Try...Catch...Finally](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md).  
  
 Las API asincrónicas en la programación de Windows Runtime tienen uno de los siguientes tipos de valor devuelto, que son similares a las tareas:  
  
-   <xref:Windows.Foundation.IAsyncOperation%601>, lo que equivale a <xref:System.Threading.Tasks.Task%601>  
  
-   <xref:Windows.Foundation.IAsyncAction>, lo que equivale a <xref:System.Threading.Tasks.Task>  
  
-   <xref:Windows.Foundation.IAsyncActionWithProgress%601>  
  
-   <xref:Windows.Foundation.IAsyncOperationWithProgress%602>  
  
 Para obtener más información y un ejemplo, vea [llamar a API asincrónicas en C# o Visual Basic](/windows/uwp/threading-async/call-asynchronous-apis-in-csharp-or-visual-basic).  
  
## <a name="BKMK_NamingConvention"></a> Convención de nomenclatura  
 Por convención, se anexa "Async" a los nombres de métodos que tengan un modificador `Async`.  
  
 Puede ignorar esta convención cuando un evento, clase base o contrato de interfaz sugieren un nombre diferente. Por ejemplo, no se debería cambiar el nombre de los controladores de eventos, tales como `Button1_Click`.  
  
## <a name="BKMK_RelatedTopics"></a> Temas relacionados y ejemplos (Visual Studio)  
  
|Título|Descripción|Ejemplo|  
|-----------|-----------------|------------|  
|[Tutorial: Acceso a la Web usando Async y Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/walkthrough-accessing-the-web-by-using-async-and-await.md)|Muestra cómo convertir una solución WPF sincrónica en una solución WPF asincrónica. La aplicación descarga una serie de sitios web.|[Async Sample: Accessing the Web Walkthrough](https://code.msdn.microsoft.com/Async-Sample-Accessing-the-9c10497f) (Ejemplo de async: Tutorial de acceso a web)|  
|[Cómo: Ampliar el tutorial de Async usando Task.WhenAll (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-extend-the-async-walkthrough-by-using-task-whenall.md)|Agrega <xref:System.Threading.Tasks.Task.WhenAll%2A?displayProperty=nameWithType> al tutorial anterior. El uso de `WhenAll` inicia todas las descargas al mismo tiempo.||  
|[Cómo: Hacer varias solicitudes Web en paralelo utilizando Async y Await (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/how-to-make-multiple-web-requests-in-parallel-by-using-async-and-await.md)|Demuestra cómo comenzar varias tareas al mismo tiempo.|[Async Sample: Make Multiple Web Requests in Parallel](https://code.msdn.microsoft.com/Async-Make-Multiple-Web-49adb82e) (Ejemplo de async: Realizar varias solicitudes web en paralelo)|  
|[Async Return Types (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/async-return-types.md) (Tipos de valor devuelto de Async [Visual Basic])|Muestra los tipos que los métodos asincrónicos pueden devolver y explica cuándo es apropiado cada uno de ellos.||  
|[Control Flow in Async Programs (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md) (Flujo de control en programas asincrónicos [Visual Basic])|Rastrea en detalle el flujo de control a través de una sucesión de expresiones await en un programa asincrónico.|[Async Sample: Control Flow in Async Programs](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0) (Ejemplo de async: Flujo de control en programas de async)|  
|[Fine-Tuning Your Async Application (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/fine-tuning-your-async-application.md) (Ajuste de una aplicación asincrónica [Visual Basic])|Muestra cómo agregar la siguiente funcionalidad a la solución asincrónica:<br /><br /> -   [Cancel an Async Task or a List of Tasks (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-an-async-task-or-a-list-of-tasks.md) (Cancelación de una tarea asincrónica o de una lista de tareas [Visual Basic])<br />-   [Cancel Async Tasks after a Period of Time (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-async-tasks-after-a-period-of-time.md) (Cancelación de tareas asincrónicas tras un período de tiempo [Visual Basic])<br />-   [Cancel Remaining Async Tasks after One Is Complete (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/cancel-remaining-async-tasks-after-one-is-complete.md) (Cancelación de tareas asincrónicas restantes [Visual Basic])<br />-   [Start Multiple Async Tasks and Process Them As They Complete (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/start-multiple-async-tasks-and-process-them-as-they-complete.md) (Inicio de varias tareas asincrónicas y cómo procesarlas a medida que se completan [Visual Basic])|[Async Sample: Fine Tuning Your Application](https://code.msdn.microsoft.com/Async-Fine-Tuning-Your-a676abea) (Ejemplo de async: Ajuste de la aplicación)|  
|[Handling Reentrancy in Async Apps (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/handling-reentrancy-in-async-apps.md) (Control de reentrada en aplicaciones asincrónicas [Visual Basic])|Muestra cómo controlar los casos en los que se reinicia una operación asincrónica activa mientras se ejecuta.||  
|[WhenAny: Bridging between the .NET Framework and the Windows Runtime](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/jj635140(v=vs.120)) (Puente entre .NET Framework y Windows Runtime)|Muestra cómo unir entre tipos de tareas en .NET Framework e IAsyncOperations en [!INCLUDE[wrt](~/includes/wrt-md.md)] para poder usar <xref:System.Threading.Tasks.Task.WhenAny%2A> con un método [!INCLUDE[wrt](~/includes/wrt-md.md)].|[Async Sample: Bridging between .NET and Windows Runtime (AsTask and WhenAny)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/jj635140(v=vs.120)) (Ejemplo de async: Puente entre .NET y Windows Runtime [AsTask y WhenAny])|  
|Async Cancellation: Bridging between the .NET Framework and the Windows Runtime (Puente entre NET. Framework y Windows Runtime)|Muestra cómo unir entre tipos de tareas en .NET Framework e IAsyncOperations en [!INCLUDE[wrt](~/includes/wrt-md.md)] para poder usar <xref:System.Threading.CancellationTokenSource> con un método [!INCLUDE[wrt](~/includes/wrt-md.md)].|[Async Sample: Bridging between .NET and Windows Runtime (AsTask & Cancellation)](https://code.msdn.microsoft.com/Async-Sample-Bridging-9479eca3) (Ejemplo de async: Puente entre .NET y Windows Runtime [AsTask y Cancellation])|  
|[Using Async for File Access (Visual Basic)](../../../../visual-basic/programming-guide/concepts/async/using-async-for-file-access.md) (Uso de Async en acceso a archivos [Visual Basic])|Enumera y demuestra los beneficios de usar async y await para obtener acceso a archivos.||  
|[Task-based Asynchronous Pattern (TAP)](../../../../standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md) (Modelo asincrónico basado en tareas [TAP])|Describe un nuevo patrón de asincronía en .NET Framework. El patrón está basado en los tipos <xref:System.Threading.Tasks.Task> y <xref:System.Threading.Tasks.Task%601>.||  
|[Vídeos de Async en Channel 9](https://channel9.msdn.com/search?term=async+&type=All)|Proporciona vínculos a una serie de vídeos sobre programación asincrónica.||  
  
## <a name="BKMK_CompleteExample"></a> Ejemplo completo  
 El código siguiente es el archivo MainWindow.xaml.vb de la aplicación de Windows Presentation Foundation (WPF) que se explica en este tema. Puede descargar el ejemplo de [Async Sample: Example from "Asynchronous Programming with Async and Await"](https://code.msdn.microsoft.com/Async-Sample-Example-from-9b9f505c) (Ejemplo de async: Ejemplo de "Programación asincrónica con Async y Await).  
  
```vb  
' Add an Imports statement and a reference for System.Net.Http  
Imports System.Net.Http  
  
Class MainWindow  
  
    ' Mark the event handler with async so you can use Await in it.  
    Private Async Sub StartButton_Click(sender As Object, e As RoutedEventArgs)  
  
        ' Call and await separately.  
        'Task<int> getLengthTask = AccessTheWebAsync();  
        '' You can do independent work here.  
        'int contentLength = await getLengthTask;  
  
        Dim contentLength As Integer = Await AccessTheWebAsync()  
  
        ResultsTextBox.Text &=  
            String.Format(vbCrLf & "Length of the downloaded string: {0}." & vbCrLf, contentLength)  
    End Sub  
  
    ' Three things to note in the signature:  
    '  - The method has an Async modifier.   
    '  - The return type is Task or Task(Of T). (See "Return Types" section.)  
    '    Here, it is Task(Of Integer) because the return statement returns an integer.  
    '  - The method name ends in "Async."  
    Async Function AccessTheWebAsync() As Task(Of Integer)  
  
        ' You need to add a reference to System.Net.Http to declare client.  
        Dim client As HttpClient = New HttpClient()  
  
        ' GetStringAsync returns a Task(Of String). That means that when you await the  
        ' task you'll get a string (urlContents).  
        Dim getStringTask As Task(Of String) = client.GetStringAsync("https://msdn.microsoft.com")  
  
        ' You can do work here that doesn't rely on the string from GetStringAsync.  
        DoIndependentWork()  
  
        ' The Await operator suspends AccessTheWebAsync.  
        '  - AccessTheWebAsync can't continue until getStringTask is complete.  
        '  - Meanwhile, control returns to the caller of AccessTheWebAsync.  
        '  - Control resumes here when getStringTask is complete.   
        '  - The Await operator then retrieves the string result from getStringTask.  
        Dim urlContents As String = Await getStringTask  
  
        ' The return statement specifies an integer result.  
        ' Any methods that are awaiting AccessTheWebAsync retrieve the length value.  
        Return urlContents.Length  
    End Function  
  
    Sub DoIndependentWork()  
        ResultsTextBox.Text &= "Working . . . . . . ." & vbCrLf  
    End Sub  
End Class  
  
' Sample Output:  
  
' Working . . . . . . .  
  
' Length of the downloaded string: 41763.  
```  
  
## <a name="see-also"></a>Vea también

- [Await (operador)](../../../../visual-basic/language-reference/operators/await-operator.md)
- [Async](../../../../visual-basic/language-reference/modifiers/async.md)
