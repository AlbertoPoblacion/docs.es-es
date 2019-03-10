---
title: Información general sobre el componente FontDialog (formularios Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- FontDialog
helpviewer_keywords:
- Font dialog box [Windows Forms], Windows Forms
- Font dialog box
- FontDialog component [Windows Forms], about FontDialog component
ms.assetid: daf46e57-1b4b-4b7a-bad0-b50ca7ba75dc
ms.openlocfilehash: 26bfb561c1050438b78c4ae0a3e6e8da32458cdd
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57725043"
---
# <a name="fontdialog-component-overview-windows-forms"></a>Información general sobre el componente FontDialog (formularios Windows Forms)
Los formularios de Windows <xref:System.Windows.Forms.FontDialog> componente es un cuadro de diálogo preconfigurado, que es el estándar Windows **fuente** cuadro de diálogo que se utiliza para exponer las fuentes que están instaladas actualmente en el sistema. Utilícelo dentro de la aplicación basada en Windows como una solución sencilla para la selección de fuente en lugar de configurar su propio cuadro de diálogo.  
  
 De forma predeterminada, el cuadro de diálogo muestra cuadros de lista para la fuente, estilo de fuente y tamaño; casillas de verificación para los efectos como tachado y subrayado; una lista desplegable para la secuencia de comandos. y un ejemplo de cómo aparecerá la fuente. (Secuencia de comandos hace referencia a scripts de distintos juegos de caracteres que están disponibles para una fuente determinada, por ejemplo, hebreo o japonés.) Para mostrar el cuadro de diálogo fuente, llame a la <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> método.  
  
## <a name="key-properties"></a>Propiedades clave  
 El componente tiene un número de propiedades que configuran su apariencia. Las propiedades que establecen las selecciones de cuadro de diálogo son <xref:System.Windows.Forms.FontDialog.Font%2A> y <xref:System.Windows.Forms.FontDialog.Color%2A>. El <xref:System.Windows.Forms.FontDialog.Font%2A> propiedad establece la fuente, estilo, tamaño, script y efectos; por ejemplo, `Arial, 10pt, style=Italic, Strikeout`.  
  
## <a name="see-also"></a>Vea también
- <xref:System.Windows.Forms.FontDialog>
- [FontDialog (componente)](fontdialog-component-windows-forms.md)
