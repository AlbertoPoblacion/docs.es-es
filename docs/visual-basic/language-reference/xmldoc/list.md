---
title: '&lt;lista&gt; (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- listheader XML tag
- <item> XML tag
- <list> XML tag
- <listheader> XML tag
- term XML tag
- list XML tag
- <description> XML tag
- description XML tag
- item XML tag
- <term> XML tag
ms.assetid: ec35fced-d58e-4520-a764-0691256e014b
ms.openlocfilehash: 8d9bcffc32a1d1670aba1ce0e7b0ff0a6dc7112d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54521119"
---
# <a name="ltlistgt-visual-basic"></a>&lt;lista&gt; (Visual Basic)
Define una lista o tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<list type="type">  
   <listheader>  
      <term>term</term>  
      <description>description</description>  
   </listheader>  
   <item>  
      <term>term</term>  
      <description>description</description>  
   </item>  
</list>  
```  
  
#### <a name="parameters"></a>Parámetros  
 `type`  
 El tipo de la lista. Debe ser un "bullet" para una lista con viñetas, "number" para una lista numerada o "table" para una tabla de dos columnas.  
  
 `term`  
 Solo se emplea para `type` es "table". Término que se define en la etiqueta de descripción.  
  
 `description`  
 Cuando `type` es "bullet" o "number", `description` es un elemento de la lista cuando `type` es "table"," `description` es la definición de `term`.  
  
## <a name="remarks"></a>Comentarios  
 El `<listheader>` bloque define el encabezado de una tabla o una definición de lista. Al definir una tabla, solo tiene que suministrar una entrada para `term` en el encabezado.  
  
 Cada elemento de la lista se especifica con un `<item>` bloque. Al crear una lista de definiciones, debe especificar ambos `term` y `description`. Sin embargo, para una tabla, lista con viñetas o lista numerada, solo tiene que suministrar una entrada para `description`.  
  
 Una lista o tabla puede tener tantos `<item>` bloquea según sea necesario.  
  
 Compile con [/doc](../../../visual-basic/reference/command-line-compiler/doc.md) para procesar los comentarios de documentación a un archivo.  
  
## <a name="example"></a>Ejemplo  
 Este ejemplo se usa el `<list>` etiqueta para definir una lista con viñetas en la sección Comentarios.  
  
 [!code-vb[VbVbcnXmlDocComments#5](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/list_1.vb)]  
  
## <a name="see-also"></a>Vea también
- [Etiquetas XML para comentarios](../../../visual-basic/language-reference/xmldoc/index.md)
