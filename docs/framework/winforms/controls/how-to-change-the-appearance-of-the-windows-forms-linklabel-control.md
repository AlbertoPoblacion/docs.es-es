---
title: Filtrar para cambiar el aspecto del control LinkLabel de formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- LinkLabel properties
- LinkLabel control [Windows Forms], changing appearance of links
- links [Windows Forms], changing appearance
- examples [Windows Forms], LinkLabel control
- LinkLabel control [Windows Forms], examples
ms.assetid: fdc5854f-5162-4457-8cbe-1042feb2d132
ms.openlocfilehash: be2f6e8e10d9f9b23b4f57fa696f1fb88c4726c0
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59105032"
---
# <a name="how-to-change-the-appearance-of-the-windows-forms-linklabel-control"></a>Filtrar para cambiar el aspecto del control LinkLabel de formularios Windows Forms
Puede cambiar el texto mostrado por el <xref:System.Windows.Forms.LinkLabel> control para adaptarse a una variedad de propósitos. Por ejemplo, es una práctica común para indicar al usuario que se puede hacer clic en texto estableciendo el texto que aparezca en un color específico con un carácter de subrayado. Después de que el usuario hace clic en el texto, el color cambia a un color diferente. Para controlar este comportamiento, puede establecer cinco propiedades diferentes: el <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A>, <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>, <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>, <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>, y <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> propiedades.  
  
### <a name="to-change-the-appearance-of-a-linklabel-control"></a>Para cambiar la apariencia de un control LinkLabel  
  
1.  Establecer el <xref:System.Windows.Forms.LinkLabel.LinkColor%2A> y <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> propiedades a los colores que desee.  
  
     Esto puede hacerse ya sea mediante programación o en tiempo de diseño en el **propiedades** ventana.  
  
    ```vb  
    ' You can set the color using decimal values for red, green, and blue  
    LinkLabel1.LinkColor = Color.FromArgb(0, 0, 255)  
    ' Or you can set the color using defined constants  
    LinkLabel1.VisitedLinkColor = Color.Purple  
    ```  
  
    ```csharp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1.LinkColor = Color.FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1.VisitedLinkColor = Color.Purple;  
    ```  
  
    ```cpp  
    // You can set the color using decimal values for red, green, and blue  
    linkLabel1->LinkColor = Color::FromArgb(0, 0, 255);  
    // Or you can set the color using defined constants  
    linkLabel1->VisitedLinkColor = Color::Purple;  
    ```  
  
2.  Establecer el <xref:System.Windows.Forms.LinkLabel.Text%2A> propiedad título apropiado.  
  
     Esto puede hacerse ya sea mediante programación o en tiempo de diseño en el **propiedades** ventana.  
  
    ```vb  
    LinkLabel1.Text = "Click here to see more."  
    ```  
  
    ```csharp  
    linkLabel1.Text = "Click here to see more.";  
    ```  
  
    ```cpp  
    linkLabel1->Text = "Click here to see more.";  
    ```  
  
3.  Establecer el <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> propiedad para determinar qué parte de la leyenda se indicará como un vínculo.  
  
     El <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> valor está representado con un <xref:System.Windows.Forms.LinkArea> que contiene dos números, la posición del carácter inicial y el número de caracteres. Esto puede hacerse ya sea mediante programación o en tiempo de diseño en el **propiedades** ventana.  
  
    ```vb  
    LinkLabel1.LinkArea = new LinkArea(6,4)  
    ```  
  
    ```csharp  
    linkLabel1.LinkArea = new LinkArea(6,4);  
    ```  
  
    ```cpp  
    linkLabel1->LinkArea = LinkArea(6,4);  
    ```  
  
4.  Establecer el <xref:System.Windows.Forms.LinkLabel.LinkBehavior%2A> propiedad <xref:System.Windows.Forms.LinkBehavior.AlwaysUnderline>, <xref:System.Windows.Forms.LinkBehavior.HoverUnderline>, o <xref:System.Windows.Forms.LinkBehavior.NeverUnderline>.  
  
     Si se establece en <xref:System.Windows.Forms.LinkBehavior.HoverUnderline>, la parte del título determinado por <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> sólo se subrayan cuando sitúe el puntero sobre él.  
  
5.  En el <xref:System.Windows.Forms.LinkLabel.LinkClicked> controlador de eventos, establezca la <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> propiedad `true`.  
  
     Cuando se ha visitado un vínculo, es una práctica común para cambiar su apariencia de alguna manera, normalmente por color. El texto cambiará al color especificado por el <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A> propiedad.  
  
    ```vb  
    Protected Sub LinkLabel1_LinkClicked (ByVal sender As Object, _  
       ByVal e As EventArgs) Handles LinkLabel1.LinkClicked  
       ' Change the color of the link text  
       ' by setting LinkVisited to True.  
       LinkLabel1.LinkVisited = True  
       ' Then do whatever other action is appropriate  
    End Sub  
    ```  
  
    ```csharp  
    protected void LinkLabel1_LinkClicked(object sender, System.EventArgs e)  
    {  
       // Change the color of the link text by setting LinkVisited   
       // to True.  
       linkLabel1.LinkVisited = true;  
       // Then do whatever other action is appropriate  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void linkLabel1_LinkClicked(System::Object ^  sender,  
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)  
       {  
          // Change the color of the link text by setting LinkVisited   
          // to True.  
          linkLabel1->LinkVisited = true;  
          // Then do whatever other action is appropriate  
       }  
    ```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.LinkLabel.LinkArea%2A>
- <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>
- <xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>
- <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A>
- [Información general sobre el control LinkLabel](linklabel-control-overview-windows-forms.md)
- [Filtrar para establecer vínculos con un objeto o página web mediante el control LinkLabel de formularios Windows Forms](link-to-an-object-or-web-page-with-wf-linklabel-control.md)
- [Control LinkLabel](linklabel-control-windows-forms.md)
