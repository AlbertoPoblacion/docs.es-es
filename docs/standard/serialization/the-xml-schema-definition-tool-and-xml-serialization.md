---
title: Herramienta de definición de esquema XML y serialización XML
ms.date: 03/30/2017
helpviewer_keywords:
- Xsd.exe
- XML serialization, XML Schema Definition tool
- XML Schema Definition tool
- serialization, XML Schema Definition tool
ms.assetid: 3c03f855-f931-47ff-bbc6-50c0367a16e4
ms.openlocfilehash: e855d3fdee5e8f37af8eaa362ecfdeea6e054bf6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645028"
---
# <a name="the-xml-schema-definition-tool-and-xml-serialization"></a>Herramienta de definición de esquema XML y serialización XML
La herramienta de definición de esquema XML ([XML Schema Definition Tool (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)) se instala junto con las herramientas de .NET Framework como parte del kit de desarrollo de software (SDK) de Windows®. La herramienta está diseñada para cumplir principalmente dos propósitos:  
  
- Para crear archivos de clase C# o para crearlos de clase Visual Basic y que así cumplan con un lenguaje de definición de esquema XML (XSD) concreto. La herramienta toma un Esquema XML como un argumento y genera un archivo que contiene varias clases que cuando se serializa con <xref:System.Xml.Serialization.XmlSerializer>, cumpla al esquema. Para obtener información sobre cómo usar la herramienta para generar clases que se ajusten a un esquema específico, vea [Cómo: Utilice la herramienta de definición de esquemas XML para generar clases y documentos de esquema XML](../../../docs/standard/serialization/xml-schema-def-tool-gen.md).  
  
- Generar un documento de esquema XML de un archivo .dll o .exe. Para ver el esquema de un conjunto de archivos que ha creado, o uno que se ha modificado con atributos, pase la DLL o el EXE como un argumento de la herramienta para generar el esquema XML. Para obtener información acerca de cómo usar la herramienta para generar un documento de esquema XML a partir de un conjunto de clases, vea [Cómo: Utilice la herramienta de definición de esquemas XML para generar clases y documentos de esquema XML](../../../docs/standard/serialization/xml-schema-def-tool-gen.md).  
  
 Para obtener más información sobre esta y otras herramientas, vea [Herramientas de .NET Framework](../../../docs/framework/tools/index.md). Para obtener más información sobre las opciones de las herramientas, consulte [XML Schema Definition Tool (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md) (Herramienta Definición de esquemas XML (Xsd.exe)).  
  
## <a name="see-also"></a>Vea también

- <xref:System.Data.DataSet>
- [Introducción a la serialización XML](../../../docs/standard/serialization/introducing-xml-serialization.md)
- [Herramienta de definición de esquema XML (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [Cómo: Serializar un objeto](../../../docs/standard/serialization/how-to-serialize-an-object.md)
- [Cómo: Deserializar un objeto](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
- [Cómo: Utilice la herramienta de definición de esquemas XML para generar clases y documentos de esquema XML](../../../docs/standard/serialization/xml-schema-def-tool-gen.md)
- [Compatibilidad con enlaces del esquema XML](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/sh1e66zd(v=vs.100))
