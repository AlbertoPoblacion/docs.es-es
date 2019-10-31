---
title: 'Cómo: iniciar una aplicación y enviarle pulsaciones de teclas: Visual Basic'
ms.date: 10/23/2019
helpviewer_keywords:
- keystrokes, sending
- Shell command example [Visual Basic]
- processes, starting and sending keystrokes
- SendKeys.SendWait examples
ms.assetid: f1303184-fce4-44fb-88b4-aac5f42d5d77
ms.openlocfilehash: 033999c07bb5839a264122b2ca330916bdf844b8
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2019
ms.locfileid: "72919392"
---
# <a name="how-to-start-an-application-and-send-it-keystrokes-visual-basic"></a>Cómo: iniciar una aplicación y enviarle pulsaciones de teclas (Visual Basic)

En este ejemplo se usa el método <xref:Microsoft.VisualBasic.Interaction.Shell%2A> para iniciar la aplicación de Bloc de notas y, después, se imprime una frase mediante el envío de pulsaciones de teclas con el método [My.Computer.Keyboard.SendKeys](xref:Microsoft.VisualBasic.Devices.Keyboard.SendKeys%2A).

## <a name="example"></a>Ejemplo

[!code-vb[VbVbalrMyComputer#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyComputer/VB/Class2.vb#25)]

## <a name="robust-programming"></a>Programación sólida

Si no se encuentra una aplicación con el identificador de proceso solicitado, se generará una excepción <xref:System.ArgumentException>.  
  
## <a name="net-framework-security"></a>Seguridad de .NET Framework

La llamada a la función `Shell` requiere plena confianza (clase <xref:System.Security.SecurityException>).

## <a name="see-also"></a>Vea también

- <xref:Microsoft.VisualBasic.Devices.Keyboard.SendKeys%2A>
- <xref:Microsoft.VisualBasic.Interaction.Shell%2A>
- <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>
