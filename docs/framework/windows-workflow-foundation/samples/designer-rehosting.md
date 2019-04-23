---
title: Rehospedaje del diseñador
ms.date: 03/30/2017
ms.assetid: b676ad31-5f64-4d84-9a36-b4d7113a2f4d
ms.openlocfilehash: b2a51014e34bf27d6f016db71d2c2eaabb906c6d
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59328171"
---
# <a name="designer-rehosting"></a>Rehospedaje del diseñador
El rehospedaje del diseñador es un escenario común que hace referencia al hospedaje del lienzo de diseño de flujo de trabajo dentro de una aplicación personalizada. La aplicación de hospedaje con la que están familiarizados la mayoría de los usuarios es Visual Studio; sin embargo, hay varios escenarios donde puede resultar útil mostrar el diseñador de flujo de trabajo en una aplicación:  
  
-   Aplicaciones de supervisión (que permiten a un usuario final visualizar el proceso, así como datos en tiempo de ejecución sobre el proceso, como el estado activo actual, los datos de tiempo de ejecución agregados o información de otro tipo sobre una instancia del flujo de trabajo).  
  
-   Aplicaciones que permiten a un usuario personalizar el proceso con un conjunto limitado de actividades.  
  
 Para admitir estos tipos de aplicaciones, el diseñador de flujo de trabajo se distribuye dentro de .NET Framework y se puede hospedar dentro de una aplicación WPF o en una aplicación Winforms con el código de hospedaje de WPF adecuado. En este ejemplo se explica cómo:  
  
-   Rehospedar el diseñador WF.  
  
-   Utilizar el cuadro de herramientas y la cuadrícula de propiedad hospedados en otro host.  
  
## <a name="rehosting-the-designer"></a>Rehospedar el diseñador  
 En este ejemplo se muestra cómo crear el diseño de WPF para contener el diseñador, que se ve en el siguiente diseño de cuadrícula (el código del cuadro de herramientas se omite por problemas de espacio). Tenga en cuenta la denominación de los bordes que contienen el diseñador y la cuadrícula de propiedad.  
  
```xaml  
<Grid>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition Width="2*"/>  
        <ColumnDefinition Width="7*"/>  
        <ColumnDefinition Width="3*"/>  
    </Grid.ColumnDefinitions>  
    <Border Grid.Column="0">  
        <sapt:ToolboxControl>...</sapt:ToolboxControl>  
    </Border>  
    <Border Grid.Column="1" Name="DesignerBorder"/>  
    <Border Grid.Column="2" Name="PropertyBorder"/>  
</Grid>  
```  
  
 A continuación, el ejemplo crea el diseñador y asocia sus propiedades <xref:System.Activities.Presentation.WorkflowDesigner.View%2A> y <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A> primarias al contenedor adecuado en la interfaz de usuario. Hay algunas líneas adicionales de código en el siguiente ejemplo que merecen explicación. La llamada a <xref:System.Activities.Core.Presentation.DesignerMetadata.Register%2A> es necesaria para asociar los diseñadores de actividad predeterminados para las actividades entregadas con [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Se llama a <xref:System.Activities.Presentation.WorkflowDesigner.Load%2A> para pasar el elemento de WF que se va a editar. Por último, las propiedades <xref:System.Activities.Presentation.WorkflowDesigner.View%2A> (lienzo primario) y <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A> (cuadrícula de propiedad) se colocan en la superficie de la interfaz de usuario.  
  
```csharp  
protected override void OnInitialized(EventArgs e)  
{  
   base.OnInitialized(e);  
   // register metadata  
   (new DesignerMetadata()).Register();  
  
   // create the workflow designer  
   WorkflowDesigner wd = new WorkflowDesigner();  
   wd.Load(new Sequence());  
   DesignerBorder.Child = wd.View;  
   PropertyBorder.Child = wd.PropertyInspectorView;  
}  
```  
  
## <a name="using-the-rehosted-toolbox"></a>Utilizar el cuadro de herramientas hospedado en otro host  
 Este ejemplo utiliza el control del cuadro de herramientas hospedado en otro host mediante declaración en XAML. Observe que en el código, se puede pasar un tipo al constructor <xref:System.Activities.Presentation.Toolbox.ToolboxItemWrapper>.  
  
```xaml  
<!-- Copyright (c) Microsoft Corporation. All rights reserved-->  
<Window x:Class="Microsoft.Samples.DesignerRehosting.RehostingWfDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sapt="clr-namespace:System.Activities.Presentation.Toolbox;assembly=System.Activities.Presentation"  
        xmlns:sys="clr-namespace:System;assembly=mscorlib"  
        Title="Window1" Height="600" Width="900">  
    <Window.Resources>  
        <sys:String x:Key="AssemblyName">System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</sys:String>  
    </Window.Resources>  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="2*"/>  
            <ColumnDefinition Width="7*"/>  
            <ColumnDefinition Width="3*"/>  
        </Grid.ColumnDefinitions>  
        <Border Grid.Column="0">  
            <sapt:ToolboxControl>  
                <sapt:ToolboxCategory CategoryName="Basic">  
                    <sapt:ToolboxItemWrapper AssemblyName="{StaticResource AssemblyName}" >  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.Sequence  
                        </sapt:ToolboxItemWrapper.ToolName>  
                       </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.WriteLine  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.If  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.While  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                </sapt:ToolboxCategory>  
            </sapt:ToolboxControl>  
        </Border>  
        <Border Grid.Column="1" Name="DesignerBorder"/>  
        <Border Grid.Column="2" Name="PropertyBorder"/>  
    </Grid>  
</Window>  
```  
  
#### <a name="using-the-sample"></a>Utilizar el ejemplo  
  
1. Abra la solución DesignerRehosting.sln en Visual Studio 2010.  
  
2. Presione F5 para compilar y ejecutar la aplicación.  
  
3. Una aplicación WPF se inicia con un diseñador hospedado en otro host.  
  
> [!IMPORTANT]
>  Puede que los ejemplos ya estén instalados en su equipo. Compruebe el siguiente directorio (predeterminado) antes de continuar.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si no existe este directorio, vaya a [Windows Communication Foundation (WCF) y Windows Workflow Foundation (WF) Samples para .NET Framework 4](https://go.microsoft.com/fwlink/?LinkId=150780) para descargar todos los Windows Communication Foundation (WCF) y [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ejemplos. Este ejemplo se encuentra en el siguiente directorio.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\DesignerRehosting\Basic`