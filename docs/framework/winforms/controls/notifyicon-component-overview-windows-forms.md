---
title: Información general sobre el componente NotifyIcon (Formularios Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- NotifyIcon
helpviewer_keywords:
- NotifyIcon component [Windows Forms], about NotifyIcon component
- system tray icons [Windows Forms], about system tray icons
- system tray icons [Windows Forms], using in Windows Forms
ms.assetid: 5b9189fa-d4ae-41a6-9b97-eb1f44bb1a69
ms.openlocfilehash: 430d869265b9add34c6de617a178aa27af6218f3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61627868"
---
# <a name="notifyicon-component-overview-windows-forms"></a>Información general sobre el componente NotifyIcon (Formularios Windows Forms)

El componente <xref:System.Windows.Forms.NotifyIcon> de Windows Forms se usa normalmente para mostrar iconos para los procesos que se ejecutan en segundo plano y no muestran una interfaz de usuario gran parte del tiempo. Un ejemplo sería un programa antivirus al que se puede acceder haciendo clic en un icono en el área de notificación de estado de la barra de tareas.

## <a name="key-properties-of-notifyicons"></a>Propiedades clave de NotifyIcons

Cada componente <xref:System.Windows.Forms.NotifyIcon> muestra un solo icono en el área de estado. Si tiene tres procesos en segundo plano y quiere mostrar un icono para cada uno, deberá agregar tres componentes <xref:System.Windows.Forms.NotifyIcon> al formulario. Las propiedades clave del componente <xref:System.Windows.Forms.NotifyIcon> son <xref:System.Windows.Forms.NotifyIcon.Icon%2A> y <xref:System.Windows.Forms.NotifyIcon.Visible%2A>. La propiedad <xref:System.Windows.Forms.NotifyIcon.Icon%2A> establece el icono que aparece en el área de estado. Para que el icono aparezca, la propiedad <xref:System.Windows.Forms.NotifyIcon.Visible%2A> debe establecerse en `true`.

## <a name="notifyicons-options"></a>Opciones de NotifyIcons

Puede asociar globos de sugerencias, menús contextuales e información sobre herramientas a un <xref:System.Windows.Forms.NotifyIcon> para ayudar al usuario.

Para mostrar globos de sugerencias para un <xref:System.Windows.Forms.NotifyIcon>, llame al método <xref:System.Windows.Forms.NotifyIcon.ShowBalloonTip%2A> y especifique el intervalo de tiempo que quiere que el globo de sugerencias se muestre. También puede especificar el texto, el icono y el título del globo de sugerencias con <xref:System.Windows.Forms.NotifyIcon.BalloonTipText%2A>, <xref:System.Windows.Forms.NotifyIcon.BalloonTipIcon%2A> y <xref:System.Windows.Forms.NotifyIcon.BalloonTipTitle%2A>, respectivamente. Los componentes <xref:System.Windows.Forms.NotifyIcon> también pueden tener asociada información sobre herramientas y menús contextuales. Para obtener más información, consulte [información general del componente ToolTip](tooltip-component-overview-windows-forms.md) y [información general del componente ContextMenu](contextmenu-component-overview-windows-forms.md).

## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.NotifyIcon>
- [NotifyIcon (componente)](notifyicon-component-windows-forms.md)