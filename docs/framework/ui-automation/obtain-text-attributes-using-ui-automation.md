---
title: Obtener atributos de texto mediante UI Automation
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- getting, text attributes
- UI Automation, getting text attributes
- text attributes, getting
ms.assetid: fdefc6c3-b836-4cfe-8dec-1484bfdc5551
ms.openlocfilehash: c338f858f1715d23cad96919db4a21a6ba49710f
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2019
ms.locfileid: "74446916"
---
# <a name="obtain-text-attributes-using-ui-automation"></a>Obtener atributos de texto mediante UI Automation
> [!NOTE]
> Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para ver la información más reciente acerca de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: automatización de la interfaz de usuario](/windows/win32/winauto/entry-uiauto-win32).  
  
 En este tema se muestra cómo usar [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] para obtener atributos de texto de un intervalo de texto. Un intervalo de texto puede corresponder a la ubicación actual del símbolo de intercalación (o selección degenerada) dentro de un documento, una selección contigua de texto, una colección de selecciones de textos inconexos o todo el contenido textual de un documento.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente se muestra cómo obtener el valor <xref:System.Windows.Automation.TextPattern.FontNameAttribute> de un intervalo de texto.  
  
 [!code-csharp[UIATextPattern_snip#StartTarget](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIATextPattern_snip/CSharp/SearchWindow.cs#starttarget)]
 [!code-vb[UIATextPattern_snip#StartTarget](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIATextPattern_snip/VisualBasic/SearchWindow.vb#starttarget)]  
[!code-csharp[UIATextPattern_snip#GetTextElement](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIATextPattern_snip/CSharp/SearchWindow.cs#gettextelement)]
[!code-vb[UIATextPattern_snip#GetTextElement](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIATextPattern_snip/VisualBasic/SearchWindow.vb#gettextelement)]  
[!code-csharp[UIATextPattern_snip#FontName](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIATextPattern_snip/CSharp/SearchWindow.cs#fontname)]
[!code-vb[UIATextPattern_snip#FontName](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIATextPattern_snip/VisualBasic/SearchWindow.vb#fontname)]  
  
 El patrón de control <xref:System.Windows.Automation.TextPattern> , junto con la clase <xref:System.Windows.Automation.Text.TextPatternRange> , admite atributos de texto básicos, propiedades y métodos. Para la funcionalidad específica del control que no es compatible con <xref:System.Windows.Automation.TextPattern> ni <xref:System.Windows.Automation.Text.TextPatternRange> , la clase <xref:System.Windows.Automation.AutomationElement>ofrece métodos para que un cliente de Automatización de la interfaz de usuario acceda al modelo de objeto nativo correspondiente.  
  
## <a name="see-also"></a>Vea también

- [Información general sobre TextPattern en Automatización de la interfaz de usuario](ui-automation-textpattern-overview.md)
- [Adición de contenido a un cuadro de texto mediante Automatización de la interfaz de usuario](add-content-to-a-text-box-using-ui-automation.md)
- [Búsqueda y resaltado de texto mediante Automatización de la interfaz de usuario](find-and-highlight-text-using-ui-automation.md)
- [Información general sobre los patrones de control de la Automatización de la interfaz de usuario](ui-automation-control-patterns-overview.md)
- [Patrones de control de Automatización de la interfaz de usuario para clientes](ui-automation-control-patterns-for-clients.md)
- [Obtención de detalles de atributos de texto diversos mediante Automatización de la interfaz de usuario](obtain-mixed-text-attribute-details-using-ui-automation.md)
