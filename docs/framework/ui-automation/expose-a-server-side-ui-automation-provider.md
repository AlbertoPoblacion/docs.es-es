---
title: Exponer un proveedor de UI Automation en el servidor
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- expose a server-side UI Automation provider
- UI Automation, server-side provider, exposing
- server-side UI Automation provider, exposing
ms.assetid: 55d419c0-2201-4101-90c9-2888df4dbb47
ms.openlocfilehash: 61515c4c87638d7e2bde63f0ca9faac58128f2e5
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59225032"
---
# <a name="expose-a-server-side-ui-automation-provider"></a>Exponer un proveedor de UI Automation en el servidor
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener información más reciente sobre [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: Automatización de interfaz de usuario](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 Este tema contiene código de ejemplo que muestra cómo exponer un proveedor de automatización de interfaz de usuario del lado servidor que se hospeda en una ventana <xref:System.Windows.Forms.Control?displayProperty=nameWithType> .  
  
 El ejemplo invalida el procedimiento de ventana para interceptar WM_GETOBJECT, que es el mensaje enviado por el servicio principal [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] cuando una aplicación cliente solicita información sobre la ventana.  
  
## <a name="example"></a>Ejemplo  
 [!code-csharp[UIAFragmentProvider_snip#116](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAFragmentProvider_snip/CSharp/ListFragment.cs#116)]
 [!code-vb[UIAFragmentProvider_snip#116](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAFragmentProvider_snip/VisualBasic/ListFragment.vb#116)]  
  
## <a name="see-also"></a>Vea también

- [Información general sobre proveedores de la Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/ui-automation-providers-overview.md)
- [Implementación del proveedor de automatización de la interfaz de usuario en el servidor](../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)
