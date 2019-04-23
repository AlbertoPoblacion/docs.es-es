---
title: Funcionamiento de las entradas mediante teclado
ms.date: 03/30/2017
helpviewer_keywords:
- keyboard input [Windows Forms], about keyboard input
- keyboards [Windows Forms], keyboard input
- Windows Forms, keyboard input
ms.assetid: 9a29433c-a180-49bb-b74c-d187786584c8
ms.openlocfilehash: ddc2f3338b231ab3ae59e65bc82c00bb8f663540
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59342179"
---
# <a name="how-keyboard-input-works"></a>Funcionamiento de las entradas mediante teclado
Los Windows Forms procesan las entradas mediante teclado provocando eventos de teclado en respuesta a los mensajes de Windows. La mayoría de las aplicaciones de Windows Forms procesan exclusivamente las entradas mediante teclado controlando los eventos de teclado. No obstante, es necesario comprender cómo funcionan los mensajes del teclado de modo que pueda implementar escenarios de entrada mediante teclado más avanzados, como interceptar teclas antes de que lleguen a un control. En este tema se describen los tipos de datos de tecla que los Windows Forms reconocen y se proporciona información general de cómo se enrutan los mensajes del teclado. Para información sobre los eventos de teclado, vea [Utilizar eventos de teclado](using-keyboard-events.md).  
  
## <a name="types-of-keys"></a>Tipos de teclas  
 Formularios de Windows identifica la entrada de teclado como códigos de teclas virtuales que están representados por el bit a bit <xref:System.Windows.Forms.Keys> enumeración. Con el <xref:System.Windows.Forms.Keys> enumeración, puede combinar una serie de teclas presionadas para producir un solo valor. Estos valores corresponden a los valores que acompañan a los mensajes de Windows WM_KEYDOWN y WM_SYSKEYDOWN. Puede detectar presiones de tecla físicas más controlando el <xref:System.Windows.Forms.Control.KeyDown> o <xref:System.Windows.Forms.Control.KeyUp> eventos. Teclas de caracteres son un subconjunto de los <xref:System.Windows.Forms.Keys> enumeración y se corresponden con los valores que acompañan a los mensajes WM_CHAR y WM_SYSCHAR Windows. Si la combinación de teclas presionadas produce un carácter, puede detectar el carácter controlando el <xref:System.Windows.Forms.Control.KeyPress> eventos. Como alternativa, puede usar <xref:Microsoft.VisualBasic.Devices.Keyboard>, expuesto por la interfaz de programación de Visual Basic, para descubrir qué teclas se han presionado y enviar las teclas. Para más información, consulte [Acceso al teclado](~/docs/visual-basic/developing-apps/programming/computer-resources/accessing-the-keyboard.md).  
  
## <a name="order-of-keyboard-events"></a>Orden de eventos de teclado  
 Como se ha indicado anteriormente, hay 3 eventos relacionados con el teclado que pueden ocurrir en un control. La secuencia siguiente muestra el orden general de los eventos:  
  
1. El usuario presiona la tecla "a", se preprocesa la tecla, se envía y un <xref:System.Windows.Forms.Control.KeyDown> se produce el evento.  
  
2. El usuario mantiene presionada la tecla "a", se preprocesa la tecla, se envía y un <xref:System.Windows.Forms.Control.KeyPress> se produce el evento.  
  
     Este evento se produce varias veces cuando el usuario mantiene presionada una tecla.  
  
3. Envía el usuario libera se preprocesa la tecla "a", la clave y un <xref:System.Windows.Forms.Control.KeyUp> se produce el evento.  
  
## <a name="preprocessing-keys"></a>Preprocesamiento de teclas  
 Como otros mensajes, se procesan los mensajes del teclado en el <xref:System.Windows.Forms.Control.WndProc%2A> método de un formulario o control. Sin embargo, antes de teclado se procesan los mensajes, el <xref:System.Windows.Forms.Control.PreProcessMessage%2A> método llama a uno o varios métodos que se pueden reemplazar para controlar teclas de caracteres especiales y teclas físicas. Puede reemplazar estos métodos para detectar y filtrar determinadas teclas antes de que el control procese los mensajes. En la tabla siguiente se muestra la acción que se realiza y el método relacionado que se produce, en el orden en que se produce el método.  
  
### <a name="preprocessing-for-a-keydown-event"></a>Preprocesamiento de un evento KeyDown  
  
|Acción|Método relacionado|Notas|  
|------------|--------------------|-----------|  
|Comprobar si es una tecla de comando como un acelerador o un método abreviado de menú.|<xref:System.Windows.Forms.Control.ProcessCmdKey%2A>|Este método procesa una tecla de comando, que tiene prioridad sobre las teclas normales. Si este método devuelve `true`, no se envía el mensaje de tecla y no se produce un evento de clave. Si devuelve `false`, <xref:System.Windows.Forms.Control.IsInputKey%2A> se denomina`.`|  
|Comprobar si hay una tecla especial que requiere preprocesamiento o una tecla de carácter normal que se debe generar un <xref:System.Windows.Forms.Control.KeyDown> eventos y se enviará a un control.|<xref:System.Windows.Forms.Control.IsInputKey%2A>|Si el método devuelve `true`, lo que significa que el control es un carácter normal y una <xref:System.Windows.Forms.Control.KeyDown> provoca el evento. Si `false`, <xref:System.Windows.Forms.Control.ProcessDialogKey%2A> se llama. **Nota:**  Para asegurarse de que un control obtiene una clave o una combinación de teclas, puede controlar la <xref:System.Windows.Forms.Control.PreviewKeyDown> evento y establecer <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A> de la <xref:System.Windows.Forms.PreviewKeyDownEventArgs> a `true` para la tecla o teclas deseadas.|  
|Comprobar si es una tecla de navegación (ESC, TAB, Retorno o teclas de flecha).|<xref:System.Windows.Forms.Control.ProcessDialogKey%2A>|Este método procesa una clave física que emplea la funcionalidad especial dentro del control, como cambiar el foco entre el control y su elemento primario. Si el control inmediato no controla la clave, el <xref:System.Windows.Forms.Control.ProcessDialogKey%2A> se llama en el control primario y así sucesivamente hasta el control de nivel superior en la jerarquía. Si este método devuelve `true`, finaliza el preprocesamiento y no se genera un evento de clave. Si devuelve `false`, un <xref:System.Windows.Forms.Control.KeyDown> se produce el evento.|  
  
### <a name="preprocessing-for-a-keypress-event"></a>Preprocesamiento de un evento KeyPress  
  
|Acción|Método relacionado|Notas|  
|------------|--------------------|-----------|  
|Comprobar si la tecla es un carácter normal que el control debería procesar.|<xref:System.Windows.Forms.Control.IsInputChar%2A>|Si el carácter es un carácter normal, este método devuelve `true`, el <xref:System.Windows.Forms.Control.KeyPress> provoca el evento y se produce la ningún preprocesamiento más. En caso contrario <xref:System.Windows.Forms.Control.ProcessDialogChar%2A> se llamará.|  
|Comprobar si el carácter es un código de tecla de acceso (como &Aceptar en un botón).|<xref:System.Windows.Forms.Control.ProcessDialogChar%2A>|Este método, similar a <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>, se llamará a la jerarquía de controles. Si el control es un control contenedor, comprueba las teclas de acceso mediante una llamada a <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> en él y sus controles secundarios. Si <xref:System.Windows.Forms.Control.ProcessDialogChar%2A> devuelve `true`, un <xref:System.Windows.Forms.Control.KeyPress> no se produce el evento.|  
  
## <a name="processing-keyboard-messages"></a>Procesamiento de mensajes del teclado  
 Después de que los mensajes de teclado alcance el <xref:System.Windows.Forms.Control.WndProc%2A> método de un formulario o control, se procesan mediante un conjunto de métodos que se pueden invalidar. Cada uno de estos métodos devuelve un <xref:System.Boolean> valor que especifica si el mensaje del teclado se procesan y consumido por el control. Si uno de los métodos devuelve `true`, se considera que se ha controlado el mensaje y no se pasa al base o primario del control para más procesamiento. De lo contrario, el mensaje permanece en la cola de mensajes y se puede procesar en otro método en el elemento base o primario del control. En la tabla siguiente se presentan los métodos que procesan los mensajes del teclado.  
  
|Método|Notas|  
|------------|-----------|  
|<xref:System.Windows.Forms.Control.ProcessKeyMessage%2A>|Este método procesa todos los mensajes de teclado que son recibidos por el <xref:System.Windows.Forms.Control.WndProc%2A> método del control.|  
|<xref:System.Windows.Forms.Control.ProcessKeyPreview%2A>|Este método envía el mensaje del teclado al elemento primario del control. Si <xref:System.Windows.Forms.Control.ProcessKeyPreview%2A> devuelve `true`, en caso contrario, no se genera ningún evento de tecla <xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A> se llama.|  
|<xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A>|Este método provoca la <xref:System.Windows.Forms.Control.KeyDown>, <xref:System.Windows.Forms.Control.KeyPress>, y <xref:System.Windows.Forms.Control.KeyUp> eventos, según corresponda.|  
  
## <a name="overriding-keyboard-methods"></a>Invalidación de métodos de teclado  
 Hay muchos métodos disponibles de invalidación cuando se preprocesa y procesa un mensaje del teclado; sin embargo, algunos métodos son opciones mucho mejores que otros. En la tabla siguiente se muestran las tareas que quizá desee llevar a cabo y la mejor forma de invalidar los métodos de teclado. Para obtener más información sobre cómo reemplazar métodos, vea [reemplazar propiedades y métodos en clases derivadas](~/docs/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md#overriding-properties-and-methods-in-derived-classes).  
  
|Tarea|Método|  
|----------|------------|  
|Intercepte una tecla de navegación y provoque un <xref:System.Windows.Forms.Control.KeyDown> eventos. Por ejemplo, desea controlar las teclas TAB y Retorno en un cuadro de texto.|Reemplace <xref:System.Windows.Forms.Control.IsInputKey%2A>. **Nota:**  También puede controlar la <xref:System.Windows.Forms.Control.PreviewKeyDown> evento y establecer <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A> de la <xref:System.Windows.Forms.PreviewKeyDownEventArgs> a `true` para la tecla o teclas deseadas.|  
|Realice entradas especiales o ejecute el control de navegación en un control. Por ejemplo, desea que el uso de las teclas de flecha en el control de lista cambie el elemento seleccionado.|Invalide <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>|  
|Intercepte una tecla de navegación y provoque un <xref:System.Windows.Forms.Control.KeyPress> eventos. Por ejemplo, en un control de cuadro de número desea que al presionar varias veces una tecla de flecha se acelere la progresión por los elementos.|Reemplace <xref:System.Windows.Forms.Control.IsInputChar%2A>.|  
|Realice el control de entrada o de navegación especial durante un <xref:System.Windows.Forms.Control.KeyPress> eventos. Por ejemplo, en un control de lista, si se mantiene presionada la tecla "r", se desplazará entre elementos que comienzan con la letra r.|Invalide <xref:System.Windows.Forms.Control.ProcessDialogChar%2A>|  
|Realice un control de tecla de acceso personalizado; por ejemplo, desea controlar las teclas de acceso en botones dibujados por el propietario contenidos en una barra de herramientas.|Reemplace <xref:System.Windows.Forms.Control.ProcessMnemonic%2A>.|  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.Keys>
- <xref:System.Windows.Forms.Control.WndProc%2A>
- <xref:System.Windows.Forms.Control.PreProcessMessage%2A>
- [My.Computer.Keyboard (objeto)](~/docs/visual-basic/language-reference/objects/my-computer-keyboard-object.md)
- [Acceso al teclado](~/docs/visual-basic/developing-apps/programming/computer-resources/accessing-the-keyboard.md)
- [Utilizar eventos de teclado](using-keyboard-events.md)
