---
title: Etiquetas XML recomendadas para comentarios de documentación
ms.date: 07/20/2015
f1_keywords:
- vb.XmlDocComment
helpviewer_keywords:
- tags, XML
- XML comments, recommended tags [Visual Basic]
- comments, recommended XML tags
ms.assetid: 294e0736-ff1e-498e-af83-6db71ed41a72
ms.openlocfilehash: 093c967557b899c8661fdec348d421996e948b94
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74352334"
---
# <a name="recommended-xml-tags-for-documentation-comments-visual-basic"></a>Etiquetas XML recomendadas para comentarios de documentación (Visual Basic)
El compilador de Visual Basic puede procesar comentarios de documentación en el código en un archivo XML. Puede usar herramientas adicionales para procesar el archivo XML en la documentación de.  
  
 Los comentarios XML se permiten en construcciones de código como tipos y miembros de tipo. En el caso de los tipos parciales, solo una parte del tipo puede tener comentarios XML, aunque no hay ninguna restricción en el comentario de sus miembros.  
  
> [!NOTE]
> Los comentarios de documentación no se pueden aplicar a espacios de nombres. La razón es que un espacio de nombres puede abarcar varios ensamblados, y no todos los ensamblados deben cargarse al mismo tiempo.  
  
 El compilador procesa cualquier etiqueta que sea XML válida. Las siguientes etiquetas proporcionan funcionalidad de uso común en la documentación del usuario.  
  
||||  
|---|---|---|  
|[\<c>](../../../visual-basic/language-reference/xmldoc/c.md)|[\<code>](../../../visual-basic/language-reference/xmldoc/code.md)|[\<example>](../../../visual-basic/language-reference/xmldoc/example.md)|  
|[\<excepción >](../../../visual-basic/language-reference/xmldoc/exception.md) <sup>1</sup>|[\<incluye >](../../../visual-basic/language-reference/xmldoc/include.md) <sup>1</sup>|[\<list>](../../../visual-basic/language-reference/xmldoc/list.md)|  
|[\<para>](../../../visual-basic/language-reference/xmldoc/para.md)|[\<param >](../../../visual-basic/language-reference/xmldoc/param.md) <sup>1</sup>|[\<paramref>](../../../visual-basic/language-reference/xmldoc/paramref.md)|  
|[\<permiso >](../../../visual-basic/language-reference/xmldoc/permission.md) <sup>1</sup>|[\<remarks>](../../../visual-basic/language-reference/xmldoc/remarks.md)|[\<returns>](../../../visual-basic/language-reference/xmldoc/returns.md)|  
|[\<consulte >](../../../visual-basic/language-reference/xmldoc/see.md) <sup>1</sup>|[\<seealso >](../../../visual-basic/language-reference/xmldoc/seealso.md) <sup>1</sup>|[\<summary>](../../../visual-basic/language-reference/xmldoc/summary.md)|  
|[\<typeparam >](../../../visual-basic/language-reference/xmldoc/typeparam.md) <sup>1</sup>|[\<value>](../../../visual-basic/language-reference/xmldoc/value.md)||  
  
 (<sup>1</sup> el compilador comprueba la sintaxis).  
  
> [!NOTE]
> Si desea que aparezcan corchetes angulares en el texto de un Comentario de documentación, use `&lt;` y `&gt;`. Por ejemplo, la cadena `"&lt;text in angle brackets&gt;"` aparecerá como `<text in angle brackets>`.  
  
## <a name="see-also"></a>Vea también

- [Documentar el código con XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
- [-doc](../../../visual-basic/reference/command-line-compiler/doc.md)
- [Crear documentación XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
