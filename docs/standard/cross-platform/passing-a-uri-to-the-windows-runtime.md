---
title: Pasar un URI a Windows Runtime
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Runtime, .NET Framework support for
- Windows Runtime, passing a URI to
ms.assetid: 3eb5ce6f-f304-4f87-8e81-0f25092f5ad4
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c489ec893ea335c8fafc904cf2a12162580ec266
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2019
ms.locfileid: "67025436"
---
# <a name="passing-a-uri-to-the-windows-runtime"></a>Pasar un URI a Windows Runtime
Los métodos de Windows Runtime solo aceptan URI absolutos. Si se pasa un URI relativo a un método en tiempo de ejecución de Windows, un <xref:System.ArgumentException> es una excepción. El motivo es el siguiente: Cuando se usa el tiempo de ejecución de Windows en el código de .NET Framework, el <xref:Windows.Foundation.Uri?displayProperty=nameWithType> clase aparece como <xref:System.Uri?displayProperty=nameWithType> en Intellisense. El <xref:System.Uri?displayProperty=nameWithType> clase permite URI relativos, pero la <xref:Windows.Foundation.Uri?displayProperty=nameWithType> clase no es así. Esto también es cierto para los métodos que expone en componentes de Windows en tiempo de ejecución. Si su componente expone un método que toma un URI, la firma de su código incluye <xref:System.Uri?displayProperty=nameWithType>. Sin embargo, para los usuarios de su componente, la firma incluye <xref:Windows.Foundation.Uri?displayProperty=nameWithType>. Un URI que se pase a su componente debe ser absoluto.  
  
En este tema se muestra cómo detectar un URI absoluto y cómo crear uno al hacer referencia a un recurso del paquete de la aplicación.  
  
## <a name="detecting-and-using-an-absolute-uri"></a>Detectar y usar un URI absoluto  
Use el <xref:System.Uri.IsAbsoluteUri%2A?displayProperty=nameWithType> propiedad para asegurarse de que un URI sea absoluto antes de pasarlo al tiempo de ejecución de Windows. Utilizar esta propiedad es más eficaz que detectar y gestionar la excepción <xref:System.ArgumentException>.  
  
## <a name="using-an-absolute-uri-for-a-resource-in-the-app-package"></a>Usar un URI absoluto para un recurso del paquete de la aplicación  
Si desea especificar un URI para un recurso incluido en el paquete de la aplicación, puede usar los esquemas `ms-appx` o `ms-appx-web` para crear un URI absoluto.  
  
El ejemplo siguiente muestra cómo establecer el <xref:Windows.UI.Xaml.Controls.WebView.Source%2A> propiedad para un <xref:Windows.UI.Xaml.Controls.WebView> control y el <xref:Windows.UI.Xaml.Controls.Image.Source%2A> propiedad para un <xref:Windows.UI.Xaml.Controls.Image> control a los recursos que se encuentran en una carpeta denominada páginas, utilizando tanto XAML como código.  
  
[!code-xaml[System.URIToWindowsURI#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml#1)]  
[!code-csharp[System.URIToWindowsURI#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml.cs#2)]
[!code-vb[System.URIToWindowsURI#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.uritowindowsuri/vb/mainpage.xaml.vb#2)]  
  
Para obtener más información sobre estos esquemas, vea [esquemas de URI](/windows/uwp/app-resources/uri-schemes) en el centro de desarrollo de Windows.  
  
## <a name="see-also"></a>Vea también

- [Compatibilidad de .NET Framework con las aplicaciones de la Tienda Windows y Windows Runtime](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
