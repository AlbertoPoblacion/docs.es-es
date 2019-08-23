---
title: Procedimiento para asociar un menú contextual con un componente NotifyIcon de formularios Windows Forms
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- context menus [Windows Forms], for background processes
- NotifyIcon component [Windows Forms], associating shortcut menus
- shortcut menus [Windows Forms], for background processes
ms.assetid: d68f3926-08d3-4f7d-949f-1981b29cf188
ms.openlocfilehash: bf5602d0526fdd97f0cc14382339095a793f13c3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922766"
---
# <a name="how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component"></a>Procedimiento para asociar un menú contextual con un componente NotifyIcon de formularios Windows Forms
> [!NOTE]
> Aunque <xref:System.Windows.Forms.MenuStrip> y <xref:System.Windows.Forms.ContextMenu> <xref:System.Windows.Forms.MainMenu> <xref:System.Windows.Forms.MainMenu> <xref:System.Windows.Forms.ContextMenu> reemplazan y agregan funcionalidad a los controles y de versiones anteriores, y se conservan por compatibilidad con versiones anteriores y uso futuro, si así lo decide. <xref:System.Windows.Forms.ContextMenuStrip>  
  
 El <xref:System.Windows.Forms.NotifyIcon> componente muestra un icono en el área de notificación de estado de la barra de tareas. Normalmente, las aplicaciones permiten hacer clic con el botón secundario en este icono para enviar comandos a la aplicación que representa. Al asociar un <xref:System.Windows.Forms.ContextMenu> componente <xref:System.Windows.Forms.NotifyIcon> al componente, puede Agregar esta funcionalidad a sus aplicaciones.  
  
> [!NOTE]
> Si desea que la aplicación se minimice en el inicio mientras se muestra una instancia del <xref:System.Windows.Forms.NotifyIcon> componente en la barra de tareas, establezca la propiedad del <xref:System.Windows.Forms.Form.WindowState%2A> formulario principal en <xref:System.Windows.Forms.FormWindowState.Minimized> y asegúrese de <xref:System.Windows.Forms.NotifyIcon> que la <xref:System.Windows.Forms.NotifyIcon.Visible%2A> propiedad del componente está establecido en `true`.  
  
### <a name="to-associate-a-shortcut-menu-with-the-notifyicon-component-at-design-time"></a>Para asociar un menú contextual con el componente NotifyIcon en tiempo de diseño  
  
1. Agregue un <xref:System.Windows.Forms.NotifyIcon> componente al formulario y establezca las propiedades importantes, como las <xref:System.Windows.Forms.NotifyIcon.Icon%2A> propiedades y <xref:System.Windows.Forms.NotifyIcon.Visible%2A> .  
  
     Para obtener más información, consulte [Cómo Agregue iconos de aplicación a la barra de tareas con el](app-icons-to-the-taskbar-with-wf-notifyicon.md)Windows Forms componente NotifyIcon.  
  
2. Agregue un <xref:System.Windows.Forms.ContextMenu> componente a su Windows Form.  
  
     Agregue elementos de menú al menú contextual que representa los comandos que desea que estén disponibles en tiempo de ejecución. También es un buen momento para agregar mejoras de menú a estos elementos de menú, como las teclas de acceso.  
  
3. Establezca la <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> propiedad <xref:System.Windows.Forms.NotifyIcon> del componente en el menú contextual que ha agregado.  
  
     Con esta propiedad establecida, el menú contextual se mostrará cuando se haga clic en el icono de la barra de tareas.  
  
### <a name="to-associate-a-shortcut-menu-with-the-notifyicon-component-programmatically"></a>Para asociar un menú contextual con el componente NotifyIcon mediante programación  
  
1. Cree una instancia de la <xref:System.Windows.Forms.NotifyIcon> clase y una <xref:System.Windows.Forms.ContextMenu> clase, con los valores de propiedad necesarios para la aplicación <xref:System.Windows.Forms.NotifyIcon> (<xref:System.Windows.Forms.NotifyIcon.Icon%2A> y <xref:System.Windows.Forms.NotifyIcon.Visible%2A> las propiedades del componente, elementos de menú para <xref:System.Windows.Forms.ContextMenu> el componente).  
  
2. Establezca la <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> propiedad <xref:System.Windows.Forms.NotifyIcon> del componente en el menú contextual que ha agregado.  
  
     Con esta propiedad establecida, el menú contextual se mostrará cuando se haga clic en el icono de la barra de tareas.  
  
    > [!NOTE]
    > En el ejemplo de código siguiente se crea una estructura de menú básica. Tendrá que personalizar las opciones de menú a las que se ajustan a la aplicación que está desarrollando. Además, querrá escribir código para controlar los <xref:System.Windows.Forms.MenuItem.Click> eventos de estos elementos de menú.  
  
    ```vb  
    Public ContextMenu1 As New ContextMenu  
    Public NotifyIcon1 As New NotifyIcon  
  
    Public Sub CreateIconMenuStructure()  
       ' Add menu items to shortcut menu.  
       ContextMenu1.MenuItems.Add("&Open Application")  
       ContextMenu1.MenuItems.Add("S&uspend Application")  
       ContextMenu1.MenuItems.Add("E&xit")  
  
       ' Set properties of NotifyIcon component.  
       NotifyIcon1.Icon = New System.Drawing.Icon _   
          (System.Environment.GetFolderPath _   
          (System.Environment.SpecialFolder.Personal)  _   
          & "\Icon.ico")  
       NotifyIcon1.Text = "Right-click me!"  
       NotifyIcon1.Visible = True  
       NotifyIcon1.ContextMenu = ContextMenu1  
    End Sub  
    ```  
  
```csharp  
public NotifyIcon notifyIcon1 = new NotifyIcon();  
public ContextMenu contextMenu1 = new ContextMenu();  
  
public void createIconMenuStructure()  
{  
   // Add menu items to shortcut menu.  
   contextMenu1.MenuItems.Add("&Open Application");  
   contextMenu1.MenuItems.Add("S&uspend Application");  
   contextMenu1.MenuItems.Add("E&xit");  
  
   // Set properties of NotifyIcon component.  
   notifyIcon1.Icon = new System.Drawing.Icon  
      (System.Environment.GetFolderPath  
      (System.Environment.SpecialFolder.Personal)  
      + @"\Icon.ico");  
   notifyIcon1.Visible = true;  
   notifyIcon1.Text = "Right-click me!";  
   notifyIcon1.Visible = true;  
   notifyIcon1.ContextMenu = contextMenu1;  
}  
```  
  
```cpp  
public:  
   System::Windows::Forms::NotifyIcon ^ notifyIcon1;  
   System::Windows::Forms::ContextMenu ^ contextMenu1;  
  
   void createIconMenuStructure()  
   {  
      // Add menu items to shortcut menu.  
      contextMenu1->MenuItems->Add("&Open Application");  
      contextMenu1->MenuItems->Add("S&uspend Application");  
      contextMenu1->MenuItems->Add("E&xit");  
  
      // Set properties of NotifyIcon component.  
      notifyIcon1->Icon = gcnew System::Drawing::Icon  
          (String::Concat(System::Environment::GetFolderPath  
          (System::Environment::SpecialFolder::Personal),  
          "\\Icon.ico"));  
      notifyIcon1->Text = "Right-click me!";  
      notifyIcon1->Visible = true;  
      notifyIcon1->ContextMenu = contextMenu1;  
   }  
```  
  
> [!NOTE]
> Debe inicializar `notifyIcon1` y `contextMenu1,` lo que puede hacer si incluye las siguientes instrucciones en el constructor del formulario:  
  
```cpp  
notifyIcon1 = gcnew System::Windows::Forms::NotifyIcon();  
contextMenu1 = gcnew System::Windows::Forms::ContextMenu();  
```  
  
## <a name="see-also"></a>Vea también

- <xref:System.Windows.Forms.NotifyIcon>
- <xref:System.Windows.Forms.NotifyIcon.Icon%2A>
- [Cómo: Agregar iconos de aplicación a la barra de tareas con el Windows Forms componente NotifyIcon](app-icons-to-the-taskbar-with-wf-notifyicon.md)
- [NotifyIcon (componente)](notifyicon-component-windows-forms.md)
- [Información general sobre el componente NotifyIcon](notifyicon-component-overview-windows-forms.md)
