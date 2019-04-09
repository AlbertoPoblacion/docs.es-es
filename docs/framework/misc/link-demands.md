---
title: Peticiones de vínculos
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET Framework], demands
- demanded permissions
- permissions [.NET Framework], demands
- granting permissions, demands
- code access security, demands
- user demands for permission
- caller security checks
- link demands
ms.assetid: a33fd5f9-2de9-4653-a4f0-d9df25082c4d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2ba3172b1a82c0a9f624a49eb63a193dd29faac1
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59166996"
---
# <a name="link-demands"></a>Peticiones de vínculos
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 Una petición de vínculo hace que se produzca una comprobación de seguridad durante la compilación Just-In-Time y comprueba solo el ensamblado de llamada inmediato del código. La vinculación se produce cuando el código se enlaza a una referencia de tipo, incluidas las referencias del puntero de función y las llamadas a métodos. Si el ensamblado de llamada no tiene permisos suficientes para vincularse al código, no se permitirá el vínculo y se producirá una excepción en tiempo de ejecución cuando se cargue y ejecute el código. Las peticiones de vínculo pueden reemplazarse en las clases que heredan de su código.  
  
 Tenga en cuenta que no se efectúa ningún recorrido de pila completo con este tipo de petición y que el código sigue siendo vulnerable a ataques. Por ejemplo, si un método en el ensamblado A está protegido por una petición de vínculo, un llamador directo del ensamblado B se evalúa según los permisos del ensamblado B.  Sin embargo, la petición de vínculo no evaluará un método del ensamblado C si llama indirectamente al método del ensamblado A con el método del ensamblado B. La petición de vínculo se especifica que solo los permisos directos en el ensamblado de llamada inmediato deben poseer un vínculo al código. No especifica los permisos que deben tener todos los llamadores para ejecutar el código.  
  
 Los modificadores de recorrido de pila <xref:System.Security.CodeAccessPermission.Assert%2A>, <xref:System.Security.CodeAccessPermission.Deny%2A> y <xref:System.Security.CodeAccessPermission.PermitOnly%2A> no afectan a la evaluación de las peticiones de vínculo.  Dado que las peticiones de vínculo no efectúan ningún recorrido de pila, los modificadores de recorrido de pila no tienen ningún efecto sobre las peticiones de vínculo.  
  
 Si se tiene acceso a un método protegido por una petición de vínculo a través de [reflexión](../../../docs/framework/reflection-and-codedom/reflection.md), a continuación, una petición de vínculo comprueba el llamador inmediato del código tiene acceso a través de reflexión. Esto es válido tanto para la detección de métodos como para la invocación de métodos efectuados por reflexión. Por ejemplo, suponga que el código usa la reflexión para devolver un <xref:System.Reflection.MethodInfo> de objeto que representa un método protegido por una petición de vínculo y, a continuación, pasa que **MethodInfo** objeto a otro código que usa el objeto para invocar el método original. En este caso, la comprobación de la petición de vínculo tiene lugar dos veces: una vez para el código que devuelve el **MethodInfo** objeto y una vez para el código que lo invoca.  
  
> [!NOTE]
>  Una petición de vínculo efectuada en un constructor de clases estáticas no protege el constructor, puesto que el sistema llama a los constructores estáticos, fuera de la ruta de acceso de ejecución del código de la aplicación. Como resultado, al aplicar una petición de vínculo a toda una clase, no puede proteger el acceso a un constructor estático, aunque proteja el resto de la clase.  
  
 El siguiente fragmento de código especifica de manera declarativa que cualquier código vinculado al método `ReadData` debe tener el permiso `CustomPermission`. Este permiso es un permiso personalizado hipotético y no existe en .NET Framework. La petición se realiza pasando un **SecurityAction.LinkDemand** marca a la `CustomPermissionAttribute`.  
  
```vb  
<CustomPermissionAttribute(SecurityAction.LinkDemand)> _  
Public Shared Function ReadData() As String  
    ' Access a custom resource.  
End Function    
```  
  
```csharp  
[CustomPermissionAttribute(SecurityAction.LinkDemand)]  
public static string ReadData()  
{  
    // Access a custom resource.  
}  
```  
  
## <a name="see-also"></a>Vea también

- [Atributos](../../../docs/standard/attributes/index.md)
- [Seguridad de acceso del código](../../../docs/framework/misc/code-access-security.md)
