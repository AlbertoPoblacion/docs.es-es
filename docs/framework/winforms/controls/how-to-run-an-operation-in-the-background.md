---
title: Procedimiento para ejecutar una operación en segundo plano
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- background tasks
- forms [Windows Forms], multithreading
- forms [Windows Forms], background operations
- background threads
- BackgroundWorker class [Windows Forms], examples
- threading [Windows Forms], background operations
- background operations
ms.assetid: 5b56e2aa-dc05-444f-930c-2d7b23f9ad5b
ms.openlocfilehash: 5ccbb6e4c09f5417f6c2766824ec7ed9722eed52
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62013340"
---
# <a name="how-to-run-an-operation-in-the-background"></a>Procedimiento para ejecutar una operación en segundo plano
Si tiene una operación que tarda mucho tiempo en completarse y no desea causar retrasos en la interfaz de usuario, puede utilizar la clase <xref:System.ComponentModel.BackgroundWorker> para ejecutar la operación en otro subproceso.  
  
 El ejemplo de código siguiente muestra cómo ejecutar en segundo plano una operación que consume mucho tiempo. El formulario cuenta con los botones **Iniciar** y **Cancelar**. Haga clic en el botón **Iniciar** para ejecutar una operación asincrónica. Haga clic en el botón **Cancelar** para detener una operación asincrónica. El resultado de cada operación se muestra en un elemento <xref:System.Windows.Forms.MessageBox>.  
  
 Visual Studio es altamente compatible con esta tarea.  
  
 Consulte también [Tutorial: Ejecución de una operación en segundo plano](walkthrough-running-an-operation-in-the-background.md).  
  
## <a name="example"></a>Ejemplo  
 [!code-csharp[System.ComponentModel.BackgroundWorker.Example#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.BackgroundWorker.Example#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilar el código  
 Para este ejemplo se necesita:  
  
- Referencias a los ensamblados System, System.Drawing y System.Windows.Forms.  
  
 Para obtener información sobre cómo compilar este ejemplo desde la línea de comandos para Visual Basic o Visual C#, vea [compilar desde la línea de comandos](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md) o [de línea de comandos con csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). También puede compilar este ejemplo en Visual Studio pegando el código en un nuevo proyecto.  
  
## <a name="see-also"></a>Vea también

- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.DoWorkEventArgs>
- [Cómo: Implementar un formulario que usa una operación en segundo plano](how-to-implement-a-form-that-uses-a-background-operation.md)
- [Componente BackgroundWorker](backgroundworker-component.md)
