---
title: Forma de documentos WordprocessingML (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 2dfb446b-5a07-4c00-9ab3-a74ba734ff3a
ms.openlocfilehash: 265da66329128e610c491c3ff50cec1bca434f6d
ms.sourcegitcommit: bce0586f0cccaae6d6cbd625d5a7b824d1d3de4b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58831818"
---
# <a name="shape-of-wordprocessingml-documents-visual-basic"></a>Forma de documentos WordprocessingML (Visual Basic)
En este tema se presenta la forma XML de un documento WordprocessingML.  
  
## <a name="microsoft-office-formats"></a>Formatos de Microsoft Office  
 El formato de archivo nativo para el sistema Microsoft Office 2007 es XML abierto de Office (comúnmente denominado XML abierto). XML abierto es un formato basado en XML que sigue la norma Ecma y que actualmente está sometido al proceso de estándares ISO-IEC. El lenguaje de marcado para los archivos de procesamiento de texto en XML abierto se denomina WordprocessingML. Este tutorial usa los archivos de origen WordprocessingML como datos para los ejemplos.  
  
 Si está utilizando Microsoft Office 2003, puede guardar documentos en el formato XML abierto de Office si ha instalado el Paquete de compatibilidad de Microsoft Office para los formatos de archivo Word, Excel y PowerPoint 2007.  
  
## <a name="the-shape-of-wordprocessingml-documents"></a>Forma de los documentos WordprocessingML  
 Lo primero que hay que comprender es la forma de los documentos WordprocessingML. Un documento WordprocessingML contiene un elemento de Body (con el nombre `w:body`) que contiene los párrafos del documento. Cada párrafo contiene una o más ejecuciones de texto (denominadas `w:r`). Cada ejecución de texto contiene uno o más fragmentos de texto (con el nombre `w:t`).  
  
 A continuación se muestra un documento WordprocessingML muy sencillo:  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<w:document  
xmlns:ve="http://schemas.openxmlformats.org/markup-compatibility/2006"  
xmlns:o="urn:schemas-microsoft-com:office:office"  
xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"  
xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math"  
xmlns:v="urn:schemas-microsoft-com:vml"  
xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing"  
xmlns:w10="urn:schemas-microsoft-com:office:word"  
xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml">  
  <w:body>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is a paragraph.</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00E22EB6"  
         w:rsidRDefault="00E22EB6">  
      <w:r>  
        <w:t>This is another paragraph.</w:t>  
      </w:r>  
    </w:p>  
  </w:body>  
</w:document>  
```  
  
 Este documento contiene dos párrafos. Contienen una ejecución de texto única y cada ejecución de texto contiene un solo fragmento de texto.  
  
 La forma más sencilla de ver el contenido de un documento WordprocessingML en forma XML es crear un documento mediante Microsoft Word, guardarlo y después ejecutar el siguiente programa que muestra XML en la consola.  
  
 Este ejemplo utiliza las clases que se encuentran en el ensamblado WindowsBase. Utiliza los tipos del espacio de nombres <xref:System.IO.Packaging?displayProperty=nameWithType>.  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
    Sub Main()  
        Dim documentRelationshipType = _  
          "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
  
        Using wdPackage As Package = _  
          Package.Open("SampleDoc.docx", _  
                       FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = wdPackage _  
                .GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri( _  
                            New Uri("/", UriKind.Relative), _  
                            docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                ' Get the officeDocument part from the package.  
                ' Load the XML in the part into an XDocument instance.  
                Dim xDoc As XDocument = _  
                    XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
                Console.WriteLine(xDoc.Root)  
            End If  
        End Using  
    End Sub  
End Module  
```  
  
## <a name="external-resources"></a>Recursos externos  
 [Introducción a los formatos de archivo Office (2007) Open XML](https://docs.microsoft.com/previous-versions/office/developer/office-2007/aa338205(v=office.12))  
  
 [Información general de WordprocessingML](https://docs.microsoft.com/previous-versions/office/developer/office-2003/aa212812(v=office.11))  
  
 [Office 2003: página de descarga de esquemas de referencia XML](https://go.microsoft.com/fwlink/?LinkId=98095)  
  
## <a name="see-also"></a>Vea también

- [Tutorial: Manipular contenido en un documento WordprocessingML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
