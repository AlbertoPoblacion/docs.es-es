---
title: Procedimiento para crear un control con enlace simple en formularios Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- data binding [Windows Forms], simple data binding
- Windows Forms controls, data binding
ms.assetid: 3bcaded8-0f1a-4cc0-8830-f59be253bf4e
ms.openlocfilehash: 79b31e61f4c7739a20765c9484db6a8cfd04b01b
ms.sourcegitcommit: 11deacc8ec9f229ab8ee3cd537515d4c2826515f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66003771"
---
# <a name="how-to-create-a-simple-bound-control-on-a-windows-form"></a>Procedimiento para crear un control con enlace simple en formularios Windows Forms
Con *enlace simple*, puede mostrar un elemento de datos único, como un valor de columna de una tabla de conjunto de datos en un control. Puede enlazar cualquier propiedad de un control de forma sencilla en un valor de datos.  
  
> [!NOTE]
>  Los cuadros de diálogo y comandos de menú que se ven pueden diferir de los descritos en la Ayuda, en función de los valores de configuración o de edición activos. Para cambiar la configuración, elija la opción **Importar y exportar configuraciones** del menú **Herramientas** . Para más información, vea [Personalizar el IDE de Visual Studio](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-simple-bind-a-control"></a>Para enlazar un control simple  
  
1. Conéctese a un origen de datos. Para obtener más información, consulte [conectarse a un origen de datos](../data/adonet/connecting-to-a-data-source.md).  
  
2. En el formulario, seleccione el control y mostrar el **propiedades** ventana.  
  
3. Expanda el **(DataBindings)** propiedad.  
  
     Las propiedades enlazadas con más frecuencia se muestran bajo el **(DataBindings)** propiedad. Por ejemplo, en la mayoría de los controles, el **texto** propiedad está enlazada con más frecuencia.  
  
4.  Si la propiedad que desea enlazar no es una de las propiedades enlazadas con frecuencia, haga clic en el **puntos suspensivos** botón (![los puntos suspensivos (...) en la ventana Propiedades de Visual Studio.](./media/how-to-create-a-simple-bound-control-on-a-windows-form/visual-studio-ellipsis-button.png)) en el **() Opciones avanzadas)** cuadro para mostrar el **formato y enlace de datos avanzado** cuadro de diálogo con una lista completa de propiedades para ese control.  
  
5. Seleccione la propiedad que desea enlazar y haga clic en la flecha desplegable situada debajo **enlace**.  
  
     Se muestra una lista de los orígenes de datos disponibles.  
  
6. Expanda el origen de datos al que desea enlazar hasta que encuentre el elemento de datos que desea. Por ejemplo, si va a enlazar a un valor de columna en la tabla de un conjunto de datos, expanda el nombre del conjunto de datos y, después, expanda el nombre de la tabla para mostrar los nombres de columna.  
  
7. Haga clic en el nombre del elemento al que se va a enlazar.  
  
8. Si estuviera trabajando la **formato y enlace de datos avanzado** cuadro de diálogo, haga clic en **Aceptar** para volver a la **propiedades** ventana.  
  
9. Si desea enlazar propiedades adicionales del control, repita los pasos del 3 al 7.  
  
    > [!NOTE]
    >  Dado que los controles de enlace simple muestran solo un único elemento de datos, es muy habitual incluir lógica de navegación en un formulario de Windows con controles de enlace simple.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.Binding>
- [Enlace de datos en Windows Forms](windows-forms-data-binding.md)
- [Enlace de datos y Windows Forms](data-binding-and-windows-forms.md)
