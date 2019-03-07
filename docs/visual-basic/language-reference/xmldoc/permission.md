---
title: <permission> (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- <permission> XML tag
- permission XML tag
ms.assetid: 0edf0500-5cd7-49c0-9255-64c48f972b77
ms.openlocfilehash: d8fe70445b2a2500f99a0156604238665b7bbd1c
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57473505"
---
# <a name="permission-visual-basic"></a>\<permiso > (Visual Basic)
Especifica un permiso necesario para el miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
<permission cref="member">description</permission>  
```  
  
## <a name="parameters"></a>Parámetros  
 `member`  
 Referencia a un miembro o campo al cual se puede llamar desde el entorno de compilación actual. El compilador comprueba si el elemento de código dado existe y traduce `member` al nombre de elemento canónico en la salida XML. Incluya `member` entre comillas ("").  
  
 `description`  
 Descripción del acceso al miembro.  
  
## <a name="remarks"></a>Comentarios  
 Use la `<permission>` etiqueta para documentar el acceso de un miembro. Use la <xref:System.Security.PermissionSet> clase para especificar el acceso a un miembro.  
  
 Compile con [/doc](../../../visual-basic/reference/command-line-compiler/doc.md) para procesar los comentarios de documentación a un archivo.  
  
## <a name="example"></a>Ejemplo  
 Este ejemplo se usa el `<permission>` etiquetas para describir que el <xref:System.Security.Permissions.FileIOPermission> requerido por la `ReadFile` método.  
  
 [!code-vb[VbVbcnXmlDocComments#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#7)]  
  
## <a name="see-also"></a>Vea también
- [Etiquetas XML para comentarios](../../../visual-basic/language-reference/xmldoc/index.md)
