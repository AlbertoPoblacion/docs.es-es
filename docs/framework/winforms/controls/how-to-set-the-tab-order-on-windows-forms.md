---
title: Filtrar para establecer el orden de tabulación en formularios Windows Forms
ms.date: 03/30/2017
f1_keywords:
- TabStop
- TabIndex
helpviewer_keywords:
- tab order [Windows Forms], controls on Windows forms
- Windows Forms controls, setting tab order
- controls [Windows Forms], setting tab order
- Windows Forms, setting tab order
ms.assetid: 71fa8e76-0472-414b-ad3c-0f90166e0ad7
ms.openlocfilehash: cd86757d43d7d57dc7777422086a7b7a96b6611e
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59162129"
---
# <a name="how-to-set-the-tab-order-on-windows-forms"></a>Filtrar para establecer el orden de tabulación en formularios Windows Forms
El orden de tabulación es el orden en el que usuario mueve el foco de un control a otro, presione la tecla TAB. Cada formulario tiene su propio orden de tabulación. De forma predeterminada, el orden de tabulación es el mismo que el orden en el que se crearon los controles. Orden de tabulación la numeración empieza por cero.  
  
> [!NOTE]
>  Los cuadros de diálogo y comandos de menú que se ven pueden diferir de los descritos en la Ayuda, en función de los valores de configuración o de edición activos. Para cambiar la configuración, elija la opción **Importar y exportar configuraciones** del menú **Herramientas** . Para más información, vea [Personalizar el IDE de Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-set-the-tab-order-of-a-control"></a>Para establecer el orden de tabulación de un control  
  
1.  En el **vista** menú, haga clic en **orden de tabulación**.  
  
     Esto activa el modo de selección de orden de tabulación del formulario. Un número (que representa el <xref:System.Windows.Forms.Control.TabIndex%2A> propiedad) aparece en la esquina superior izquierda de cada control.  
  
2.  Haga clic en los controles de forma secuencial para establecer el orden de tabulación que desee.  
  
    > [!NOTE]
    >  Posición de un control en el orden de tabulación puede establecerse en cualquier valor mayor o igual que 0. Cuando se produzcan duplicados, se evalúa el orden z de los dos controles y el control en la parte superior se pone en primer lugar. (El orden z es el diseño visual de los controles en un formulario de eje z del formulario [profundidad]. El orden z determina qué controles están delante de otros controles.) Para obtener más información acerca del orden z, vea [disponer objetos en Windows Forms](how-to-layer-objects-on-windows-forms.md).  
  
3.  Cuando haya terminado, haga clic en **orden de tabulación** en el **vista** nuevo menú para abandonar el modo de orden de tabulación.  
  
    > [!NOTE]
    >  Los controles que no se pueden obtener el foco, así como los controles deshabilitados e invisibles, no tiene un <xref:System.Windows.Forms.Control.TabIndex%2A> propiedad y no se incluyen en el orden de tabulación. Cuando el usuario presiona la tecla TAB, se omiten estos controles.  
  
 Como alternativa, se puede establecer el orden de tabulación en la ventana de propiedades mediante el <xref:System.Windows.Forms.Control.TabIndex%2A> propiedad. El <xref:System.Windows.Forms.Control.TabIndex%2A> propiedad de un control determina dónde se coloca en el orden de tabulación. De forma predeterminada, el primer control dibujado tiene un <xref:System.Windows.Forms.Control.TabIndex%2A> valor de 0, el segundo tiene un <xref:System.Windows.Forms.Control.TabIndex%2A> de 1 y así sucesivamente.  
  
 Además, de forma predeterminada, un <xref:System.Windows.Forms.GroupBox> control tiene su propio <xref:System.Windows.Forms.Control.TabIndex%2A> valor, que es un número entero. Un <xref:System.Windows.Forms.GroupBox> propio control no tiene el foco en tiempo de ejecución. Por lo tanto, cada control dentro de un <xref:System.Windows.Forms.GroupBox> tiene su propio decimal <xref:System.Windows.Forms.Control.TabIndex%2A> valor, comenzando con.0. Naturalmente, como el <xref:System.Windows.Forms.Control.TabIndex%2A> de un <xref:System.Windows.Forms.GroupBox> se incrementa el control, los controles que se aumentará en consecuencia. Si ha cambiado una <xref:System.Windows.Forms.Control.TabIndex%2A> valor comprendido entre 5 y 6, el <xref:System.Windows.Forms.Control.TabIndex%2A> cambia automáticamente el valor del primer control en su grupo a 6.0 y así sucesivamente.  
  
 Por último, se puede omitir cualquier control de los muchos en el formulario en el orden de tabulación. Por lo general, al presionar TAB consecutivamente en tiempo de ejecución selecciona cada control en el orden de tabulación. Si se desactiva el <xref:System.Windows.Forms.Control.TabStop%2A> propiedad, puede hacer que un control se pase por alto en el orden de tabulación del formulario.  
  
#### <a name="to-remove-a-control-from-the-tab-order"></a>Para quitar un control del orden de tabulación  
  
1.  Establecer el control <xref:System.Windows.Forms.Control.TabStop%2A> propiedad `false` en la ventana Propiedades.  
  
     Un control cuya <xref:System.Windows.Forms.Control.TabStop%2A> se ha establecido la propiedad en `false` todavía mantiene su posición en el orden de tabulación, aunque se omita al recorrer los controles con la tecla TAB.  
  
    > [!NOTE]
    >  Un grupo de botones de radio tiene una sola pestaña de tabulación en tiempo de ejecución. El botón seleccionado (es decir, el botón con su <xref:System.Windows.Forms.RadioButton.Checked%2A> propiedad establecida en `true`) tiene su <xref:System.Windows.Forms.Control.TabStop%2A> propiedad se establece automáticamente en `true`, mientras que los demás botones tienen sus <xref:System.Windows.Forms.Control.TabStop%2A> propiedad establecida en `false`. Para obtener más información acerca de la agrupación <xref:System.Windows.Forms.RadioButton> los controles, vea [agrupar controles RadioButton de formularios Windows Forms para que funcionen como un conjunto](how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md).  
  
## <a name="see-also"></a>Vea también

- [Controles de Windows Forms](index.md)
- [Organizar controles en formularios Windows Forms](arranging-controls-on-windows-forms.md)
- [Controles que se utilizan en formularios Windows Forms](controls-to-use-on-windows-forms.md)
- [Controles de formularios Windows Forms por función](windows-forms-controls-by-function.md)
