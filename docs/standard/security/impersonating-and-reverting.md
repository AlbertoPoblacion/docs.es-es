---
title: Suplantar y revertir
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WindowsIdentity objects, impersonating
- security [.NET Framework], impersonating Windows accounts
- impersonating Windows accounts
ms.assetid: b93d402c-6c28-4f50-b2bc-d9607dc3e470
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 97b15ea2202ca410dd517db63a7145d27f62bb48
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59338415"
---
# <a name="impersonating-and-reverting"></a>Suplantar y revertir
En ocasiones es posible que deba obtener un token de cuenta de Windows para suplantar una cuenta de Windows. Por ejemplo, la aplicación basada en ASP.NET podría tener que actuar en nombre de varios usuarios en momentos distintos. La aplicación podría aceptar un token que represente un administrador de Internet Information Services (IIS), suplantar al usuario, realizar una operación y revertir a la identidad anterior. A continuación, podría aceptar un token de IIS que represente a un usuario con menos derechos, realizar alguna operación y revertir de nuevo.  
  
 En situaciones donde la aplicación deba suplantar una cuenta de Windows que IIS no haya asociado al subproceso actual, debe recuperar el token de esa cuenta y usarlo para activar la cuenta. Para ello, debe realizar las siguientes tareas:  
  
1. Recupere un token de cuenta de un usuario concreto haciendo una llamada al método **LogonUser** no administrado. Este método no está en la biblioteca de clases base de .NET Framework, pero se encuentra en el archivo **advapi32.dll** no administrado. El acceso a métodos en código no administrado es una operación avanzada y queda fuera del ámbito de este contenido. Para más información, consulte [Interoperating with Unmanaged Code](../../../docs/framework/interop/index.md) (Interoperar con código no administrado) Para más información sobre el método **LogonUser** y el archivo **advapi32.dll**, consulte la documentación de Platform SDK.  
  
2. Cree una nueva instancia de la clase **WindowsIdentity**, pasando el token. En el siguiente código se muestra esta llamada, donde `hToken` representa un token de Windows.  
  
    ```csharp  
    WindowsIdentity impersonatedIdentity = new WindowsIdentity(hToken);  
    ```  
  
    ```vb  
    Dim impersonatedIdentity As New WindowsIdentity(hToken)  
    ```  
  
3. Comience la suplantación con la creación de una nueva instancia de la clase <xref:System.Security.Principal.WindowsImpersonationContext> e inicialícela con el método <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A?displayProperty=nameWithType> de la clase inicializada, como se muestra en el código siguiente.  
  
    ```csharp  
    WindowsImpersonationContext myImpersonation = impersonatedIdentity.Impersonate();  
    ```  
  
    ```vb  
    WindowsImpersonationContext myImpersonation = impersonatedIdentity.Impersonate()  
    ```  
  
4. Cuando ya no necesite suplantar, llame al método <xref:System.Security.Principal.WindowsImpersonationContext.Undo%2A?displayProperty=nameWithType> para revertir la suplantación, como se muestra en el código siguiente.  
  
    ```csharp  
    myImpersonation.Undo();  
    ```  
  
    ```vb  
    myImpersonation.Undo()  
    ```  
  
 Si ya ha asociado el código de confianza un <xref:System.Security.Principal.WindowsPrincipal> objeto al subproceso, puede llamar al método de instancia **Impersonate**, que no toma un token de cuenta. Tenga en cuenta que esto solo es útil cuando el objeto **WindowsPrincipal** del subproceso representa a un usuario que no es en el que se está ejecutando el proceso. Por ejemplo, podría encontrarse con esta situación si usa ASP.NET con la autenticación de Windows activada y la suplantación desactivada. En este caso, el proceso se ejecuta en una cuenta configurada en Internet Information Services (IIS) mientras la entidad de seguridad actual representa al usuario de Windows que está accediendo a la página.  
  
 Tenga en cuenta que ni **Impersonate** ni **deshacer** cambios el **Principal** objeto (<xref:System.Security.Principal.IPrincipal>) asociado al contexto de llamada actual. En su lugar, la suplantación y la reversión cambian el token asociado con el proceso de sistema operativo actual.  
  
## <a name="see-also"></a>Vea también

- <xref:System.Security.Principal.WindowsIdentity>
- <xref:System.Security.Principal.WindowsImpersonationContext>
- [Objetos Principal e Identity](../../../docs/standard/security/principal-and-identity-objects.md)
- [Interoperar con código no administrado](../../../docs/framework/interop/index.md)
