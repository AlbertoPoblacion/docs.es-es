---
title: Procedimiento para agregar información personalizada a los controles TreeView o ListView (formularios Windows Forms)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- ListItem
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- examples [Windows Forms], ListView control
- ListView control [Windows Forms], adding custom information
- TreeView control [Windows Forms], adding custom information
ms.assetid: 68be11de-1d5b-430e-901f-cfbe48d14b19
ms.openlocfilehash: 302eb1b88d4e43b4e2bd6395e27a3a6489320085
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61640408"
---
# <a name="how-to-add-custom-information-to-a-treeview-or-listview-control-windows-forms"></a>Procedimiento para agregar información personalizada a los controles TreeView o ListView (formularios Windows Forms)
Puede crear un nodo derivado en un formulario Windows Forms <xref:System.Windows.Forms.TreeView> control o un elemento derivado en un <xref:System.Windows.Forms.ListView> control. La derivación permite agregar cualquier campo que se necesite, así como métodos personalizados y constructores para controlarlos. Uno de los usos de esta característica consiste en adjuntar un objeto Customer a cada nodo de árbol o elemento de lista. Los ejemplos siguientes son para un <xref:System.Windows.Forms.TreeView> control, pero el mismo enfoque se puede usar para un <xref:System.Windows.Forms.ListView> control.  
  
### <a name="to-derive-a-tree-node"></a>Para derivar un nodo de árbol  
  
- Cree una nueva clase de nodo, derivada de la <xref:System.Windows.Forms.TreeNode> (clase), que tiene un campo personalizado para registrar una ruta de acceso de archivo.  
  
    ```vb  
    Class myTreeNode  
       Inherits TreeNode  
  
       Public FilePath As String  
  
       Sub New(ByVal fp As String)  
          MyBase.New()  
          FilePath = fp  
          Me.Text = fp.Substring(fp.LastIndexOf("\"))  
       End Sub  
    End Class  
    ```  
  
    ```csharp  
    class myTreeNode : TreeNode  
    {  
       public string FilePath;  
  
       public myTreeNode(string fp)  
       {  
          FilePath = fp;  
          this.Text = fp.Substring(fp.LastIndexOf("\\"));  
       }  
    }  
    ```  
  
    ```cpp  
    ref class myTreeNode : public TreeNode  
    {  
    public:  
       System::String ^ FilePath;  
  
       myTreeNode(System::String ^ fp)  
       {  
          FilePath = fp;  
          this->Text = fp->Substring(fp->LastIndexOf("\\"));  
       }  
    };  
    ```  
  
### <a name="to-use-a-derived-tree-node"></a>Para utilizar un nodo de árbol derivado  
  
1. Puede utilizar el nuevo nodo de árbol derivado como parámetro para llamadas de función.  
  
     En el ejemplo siguiente, la ruta de acceso establecida para la ubicación del archivo de texto es la carpeta Mis documentos. Se utiliza esta ubicación porque se puede suponer que la mayoría de los equipos que ejecuten el sistema operativo Windows tendrán este directorio. Esto permite también a los usuarios con niveles de acceso mínimos ejecutar la aplicación de forma segura.  
  
    ```vb  
    ' You should replace the bold text file   
    ' in the sample below with a text file of your own choosing.  
    TreeView1.Nodes.Add(New myTreeNode (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\ TextFile.txt ") )  
    ```  
  
    ```csharp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    treeView1.Nodes.Add(new myTreeNode (System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       + @"\TextFile.txt") );  
    ```  
  
    ```cpp  
    // You should replace the bold text file   
    // in the sample below with a text file of your own choosing.  
    treeView1->Nodes->Add(new myTreeNode(String::Concat(  
       System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\TextFile.txt")));  
    ```  
  
2. Si se pasa el nodo de árbol y se escribe como un <xref:System.Windows.Forms.TreeNode> clase, a continuación, tendrá que convertirlo a la clase derivada. La conversión de tipos es una conversión explícita de un tipo de objeto a otro. Para obtener más información sobre la conversión, consulte [conversiones implícitas y explícitas](~/docs/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md) (Visual Basic), [() operador](~/docs/csharp/language-reference/operators/invocation-operator.md) (Visual C#), o [operador de conversión: ()](/cpp/cpp/cast-operator-parens) ([!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) .  
  
    ```vb  
    Public Sub TreeView1_AfterSelect(ByVal sender As Object, ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       Dim mynode As myTreeNode  
       mynode = CType(e.node, myTreeNode)  
       MessageBox.Show("Node selected is " & mynode.filepath)  
    End Sub  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,  
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       myTreeNode myNode = (myTreeNode)e.Node;  
       MessageBox.Show("Node selected is " + myNode.FilePath);  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          myTreeNode ^ myNode = safe_cast<myTreeNode^>(e->Node);  
          MessageBox::Show(String::Concat("Node selected is ",   
             myNode->FilePath));  
       }  
    ```  
  
## <a name="see-also"></a>Vea también

- [TreeView (control)](treeview-control-windows-forms.md)
- [ListView (Control)](listview-control-windows-forms.md)
