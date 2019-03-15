---
title: Ampliar el marco de vidrio en una aplicación de WPF
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applications [WPF], extending glass frames into
- graphics [WPF], extending glass frames into applications
- extending glass frames into applications [WPF]
- glass frames [WPF], extending into applications
ms.assetid: 74388a3a-4b69-4a9d-ba1f-e107636bd660
ms.openlocfilehash: d7a00f2508769534e49c965d098dbacb01a1f189
ms.sourcegitcommit: 69bf8b719d4c289eec7b45336d0b933dd7927841
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/14/2019
ms.locfileid: "57843537"
---
# <a name="extend-glass-frame-into-a-wpf-application"></a>Ampliar el marco de vidrio en una aplicación de WPF

En este tema muestra cómo extender el [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)] marco de vidrio en el área de cliente de una aplicación de Windows Presentation Foundation (WPF).

> [!NOTE]
> Este ejemplo solo funciona en una máquina [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] que ejecute el Administrador de ventanas de escritorio (DWM) con efecto de cristal habilitado. [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] Home Basic no admite el efecto de cristal transparente. Las áreas que normalmente se representarían con el efecto de cristal transparente en otras ediciones de [!INCLUDE[TLA2#tla_winvista](../../../../includes/tla2sharptla-winvista-md.md)] se representan opacas.

## <a name="example"></a>Ejemplo

En la siguiente imagen se muestra el marco de vidrio ampliado en la barra de direcciones de Internet Explorer 7.

**Internet Explorer con marco de cristal ampliado detrás de la barra de direcciones.**

![IE7 con marco de cristal ampliado detrás de la barra de direcciones.](./media/ie7glasstopbar.PNG "IE7glasstopbar")

Para ampliar el marco de cristal en una aplicación [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] se requiere acceso a la [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] no administrada. El siguiente ejemplo de código realiza una invocación de plataforma (pinvoke) para las dos [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] necesarias para ampliar el marco en el área cliente. Cada una de estas [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] se declaran en una clase denominada **NonClientRegionAPI**.

```csharp
[StructLayout(LayoutKind.Sequential)]
public struct MARGINS
{
    public int cxLeftWidth;      // width of left border that retains its size
    public int cxRightWidth;     // width of right border that retains its size
    public int cyTopHeight;      // height of top border that retains its size
    public int cyBottomHeight;   // height of bottom border that retains its size
};

[DllImport("DwmApi.dll")]
public static extern int DwmExtendFrameIntoClientArea(
    IntPtr hwnd,
    ref MARGINS pMarInset);
```

```vb
<StructLayout(LayoutKind.Sequential)>
Public Structure MARGINS
    Public cxLeftWidth As Integer ' width of left border that retains its size
    Public cxRightWidth As Integer ' width of right border that retains its size
    Public cyTopHeight As Integer ' height of top border that retains its size
    Public cyBottomHeight As Integer ' height of bottom border that retains its size
End Structure

<DllImport("DwmApi.dll")>
Public Shared Function DwmExtendFrameIntoClientArea(ByVal hwnd As IntPtr, ByRef pMarInset As MARGINS) As Integer
End Function
```

[DwmExtendFrameIntoClientArea](/windows/desktop/api/dwmapi/nf-dwmapi-dwmextendframeintoclientarea) es la función de DWM que amplia el marco en el área cliente. Toma dos parámetros; un identificador de ventana y una estructura [MARGINS](/windows/desktop/api/uxtheme/ns-uxtheme-_margins). [MARGINS](/windows/desktop/api/uxtheme/ns-uxtheme-_margins) se usa para indicarle al DWM cuánto más debe ampliarse el marco en el área cliente.

## <a name="example"></a>Ejemplo

Para usar la función [DwmExtendFrameIntoClientArea](/windows/desktop/api/dwmapi/nf-dwmapi-dwmextendframeintoclientarea), debe obtenerse un identificador de ventana. En [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)], se puede obtener el identificador de ventana de la <xref:System.Windows.Interop.HwndSource.Handle%2A> propiedad de un <xref:System.Windows.Interop.HwndSource>. En el ejemplo siguiente, el marco se extiende en el área de cliente en el <xref:System.Windows.FrameworkElement.Loaded> eventos de la ventana.

```csharp
void OnLoaded(object sender, RoutedEventArgs e)
{
   try
   {
      // Obtain the window handle for WPF application
      IntPtr mainWindowPtr = new WindowInteropHelper(this).Handle;
      HwndSource mainWindowSrc = HwndSource.FromHwnd(mainWindowPtr);
      mainWindowSrc.CompositionTarget.BackgroundColor = Color.FromArgb(0, 0, 0, 0);

      // Get System Dpi
      System.Drawing.Graphics desktop = System.Drawing.Graphics.FromHwnd(mainWindowPtr);
      float DesktopDpiX = desktop.DpiX;
      float DesktopDpiY = desktop.DpiY;

      // Set Margins
      NonClientRegionAPI.MARGINS margins = new NonClientRegionAPI.MARGINS();

      // Extend glass frame into client area
      // Note that the default desktop Dpi is 96dpi. The  margins are
      // adjusted for the system Dpi.
      margins.cxLeftWidth = Convert.ToInt32(5 * (DesktopDpiX / 96));
      margins.cxRightWidth = Convert.ToInt32(5 * (DesktopDpiX / 96));
      margins.cyTopHeight = Convert.ToInt32(((int)topBar.ActualHeight + 5) * (DesktopDpiX / 96));
      margins.cyBottomHeight = Convert.ToInt32(5 * (DesktopDpiX / 96));

      int hr = NonClientRegionAPI.DwmExtendFrameIntoClientArea(mainWindowSrc.Handle, ref margins);
      //
      if (hr < 0)
      {
         //DwmExtendFrameIntoClientArea Failed
      }
   }
   // If not Vista, paint background white.
   catch (DllNotFoundException)
   {
      Application.Current.MainWindow.Background = Brushes.White;
   }
}
```

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra una ventana simple en la que el marco se amplía en el área cliente. El marco se amplía por detrás del borde superior que contiene las dos <xref:System.Windows.Controls.TextBox> objetos.

```xaml
<Window x:Class="SDKSample.Window1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Extended Glass in WPF" Height="300" Width="400"
    Loaded="OnLoaded" Background="Transparent"
    >
  <Grid ShowGridLines="True">
    <DockPanel Name="mainDock">
      <!-- The border is used to compute the rendered height with margins.
           topBar contents will be displayed on the extended glass frame.-->
      <Border Name="topBar" DockPanel.Dock="Top" >
        <Grid Name="grid">
          <Grid.ColumnDefinitions>
            <ColumnDefinition MinWidth="100" Width="*"/>
            <ColumnDefinition Width="Auto"/>
          </Grid.ColumnDefinitions>
          <TextBox Grid.Column="0" MinWidth="100" Margin="0,0,10,5">Path</TextBox>
          <TextBox Grid.Column="1" MinWidth="75" Margin="0,0,0,5">Search</TextBox>
        </Grid>
      </Border>
      <Grid DockPanel.Dock="Top" >
        <Grid.ColumnDefinitions>
          <ColumnDefinition/>
        </Grid.ColumnDefinitions>
        <TextBox Grid.Column="0" AcceptsReturn="True"/>
      </Grid>
    </DockPanel>
  </Grid>
</Window>
```

En la siguiente imagen se muestra el marco de vidrio ampliado en una aplicación [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)].

**Marco de vidrio ampliado en una**  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]**aplicación**.

![Marco de vidrio ampliado en una aplicación WPF.](./media/wpfextendedglassintoclient.PNG "WPFextendedGlassIntoClient")

## <a name="see-also"></a>Vea también

- [Información general del Administrador de ventanas de escritorio](/windows/desktop/dwm/dwm-overview)
- [Información general de desenfoque del Administrador de ventanas de escritorio](/windows/desktop/dwm/blur-ovw)
- [DwmExtendFrameIntoClientArea](/windows/desktop/api/dwmapi/nf-dwmapi-dwmextendframeintoclientarea) (DwmExtendFrameIntoClientArea [función])
