---
title: Seguridad de acceso del código
ms.date: 03/30/2017
helpviewer_keywords:
- named permission sets, code access security
- call stacks
- malicious code
- stack walk
- security [.NET Framework], code access security
- permissions [.NET Framework], code access security
- trusted code
- mobile code security
- unmanaged code, code access security
- granting permissions, code access security
- user authentication, code access security
- code access security
ms.assetid: 859af632-c80d-4736-8d6f-1e01b09ce127
author: mairaw
ms.author: mairaw
ms.openlocfilehash: aa256fe95013494488ff52258186763fab7a85c9
ms.sourcegitcommit: 518e7634b86d3980ec7da5f8c308cc1054daedb7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/01/2019
ms.locfileid: "66456658"
---
# <a name="code-access-security"></a>Seguridad de acceso del código
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 Los equipos conectados de hoy en día suelen estar expuestos a código procedente de varios orígenes, posiblemente desconocidos. Código puede adjunto a correo electrónico, incluirse en documentos o descargado a través de Internet. Por desgracia, muchos usuarios de equipos han experimentado personalmente las consecuencias del código móvil malintencionado, como virus y gusanos, que pueden dañar o destruir datos y costar tiempo y dinero.  
  
 Los mecanismos de seguridad más comunes conceden derechos a los usuarios según sus credenciales de inicio de sesión (normalmente, una contraseña) y limitan los recursos (a menudo, directorios y archivos) a los que puede acceder el usuario. Sin embargo, este enfoque no soluciona algunos problemas: los usuarios obtienen el código de muchos orígenes, algunos de los cuales pueden ser confiables. Además, el código puede contener errores o vulnerabilidades que permitan que lo explote el código malintencionado y el usuario, a veces, no sabe cómo actuará el código. En consecuencia, los equipos pueden resultar dañados y se pueden perder datos privados si un usuario precavido y de confianza ejecuta software malintencionado o que contenga errores. La mayoría de los mecanismos de seguridad de los sistemas operativos requiere que cada fragmento de código sea de plena confianza para ejecutarse, con la excepción, quizás, de los scripts de una página web. Por lo tanto, sigue siendo necesario un mecanismo de seguridad de amplia aplicación que permita que el código que se origina en un equipo se ejecute con protección en otro sistema, aunque no haya ninguna relación de confianza entre los sistemas.  
  
 .NET Framework proporciona un mecanismo de seguridad denominado “seguridad de acceso del código” para contribuir a proteger los sistemas informáticos del código móvil malintencionado, permitir que el código de origen desconocido se ejecute con protección y evitar que el código de confianza ponga en riesgo la seguridad, ya sea de manera intencionada o accidental. La seguridad de acceso del código proporciona al código varios grados de confianza, dependiendo de su procedencia y de otros aspectos de la identidad del código. La seguridad de acceso del código también exige al código los distintos niveles de confianza, lo que reduce la cantidad de código que debe ser de plena confianza para ejecutarse. Al utilizar la seguridad de acceso del código, se puede reducir la probabilidad de que un código malintencionado o con errores use el código de la forma que no debe. Puede reducir su responsabilidad, ya que usted puede especificar el conjunto de operaciones que debe poder realizar el código. La seguridad de acceso del código también puede contribuir a minimizar el daño que puede derivarse de las vulnerabilidades de seguridad en el código.  
  
> [!NOTE]
>  Se realizaron cambios importantes en la seguridad de acceso del código en [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]. El cambio más notable ha sido [transparencia en seguridad](../../../docs/framework/misc/security-transparent-code.md), pero también hay otros cambios importantes que afectan a la seguridad de acceso del código. Para obtener información acerca de estos cambios, consulte [cambios de seguridad](../../../docs/framework/security/security-changes.md).  
  
 La seguridad de acceso del código afecta, principalmente, al código de las bibliotecas y a las aplicaciones de confianza parcial. Los desarrolladores de bibliotecas deben proteger sus códigos del acceso no autorizado desde las aplicaciones de confianza parcial. Las aplicaciones de confianza parcial son aplicaciones que se cargan desde orígenes externos, como Internet. Las aplicaciones que se instalan en el escritorio o en la intranet local se ejecutan con plena confianza. Aplicaciones de plena confianza no se ven afectadas por la seguridad de acceso del código, a menos que se marcan como [transparente en seguridad](../../../docs/framework/misc/security-transparent-code.md), ya que son de plena confianza. La única limitación de las aplicaciones de plena confianza es que las aplicaciones marcadas con el atributo <xref:System.Security.SecurityTransparentAttribute> no pueden llamar al código marcado con el atributo <xref:System.Security.SecurityCriticalAttribute>. Las aplicaciones de confianza parcial se deben ejecutar en un espacio aislado (por ejemplo, en Internet Explorer) para que se pueda aplicar la seguridad de acceso del código. Si descarga una aplicación de Internet y vuelva a ejecutarlo desde el escritorio, obtendrá un <xref:System.NotSupportedException> con el mensaje: "Se ha intentado cargar un ensamblado desde una ubicación de red que habría provocado el ensamblado se encuentre en un espacio aislado en versiones anteriores de .NET Framework. Esta versión de .NET Framework no habilita la directiva CAS de forma predeterminada, por lo que esta carga puede ser peligrosa”. Si está seguro de que se puede confiar en la aplicación, puede habilitarlo para ejecutarse como de plena confianza mediante el uso de la [ \<loadFromRemoteSources > elemento](../../../docs/framework/configure-apps/file-schema/runtime/loadfromremotesources-element.md). Para obtener información acerca de cómo ejecutar una aplicación en un espacio aislado, vea [Cómo: Ejecutar código de confianza parcial en un espacio aislado](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
 Todo el código administrado que tiene como destino el Common Language Runtime se beneficia de la seguridad de acceso del código, aunque ese código no haga ni una sola llamada de seguridad de acceso del código. Para obtener más información, vea [Code Access Security Basics](../../../docs/framework/misc/code-access-security-basics.md) (Aspectos básicos de seguridad de acceso del código).  
  
<a name="key_functions"></a>   
## <a name="key-functions-of-code-access-security"></a>Funciones clave de la seguridad de acceso del código  
 La seguridad de acceso del código contribuye a limitar el acceso que tiene el código a operaciones y recursos protegidos. En .NET Framework, la seguridad de acceso del código realiza las funciones siguientes:  
  
- Define permisos y conjuntos de permisos que representan el derecho de acceso a varios recursos del sistema.  
  
- Permite que el código exija que sus llamadores tengan permisos específicos.  
  
- Permite que el código exija que sus llamadores posean una firma digital, por lo que solo los llamadores de una organización o un sitio concretos pueden llamar al código protegido.  
  
- Impone restricciones en el código en tiempo de ejecución mediante la comparación de los permisos concedidos a cada llamador en la pila de llamadas con los permisos que deben poseer.  
  
<a name="walking_the_call_stack"></a>   
## <a name="walking-the-call-stack"></a>Recorrido de la pila de llamadas  
 Para averiguar si el código tiene autorización para acceder a un recurso o para ejecutar una operación, el sistema de seguridad en tiempo de ejecución recorre la pila de llamadas y compara los permisos concedidos a cada llamador con el permiso que se pide. Si algún llamador de la pila de llamadas no tiene el permiso solicitado, se iniciará una excepción de seguridad y se rechazará el acceso. El recorrido de la pila está diseñado para evitar los ataques por señuelo, en los que el código de menor confianza llama a código de confianza alta y lo utiliza para realizar acciones no autorizadas. La solicitud de permisos a todos los llamadores en tiempo de ejecución afecta al rendimiento, pero es esencial para proteger el código de los ataques por señuelo del código de menor confianza. Para optimizar el rendimiento, puede hacer que el código realice menos recorridos de la pila. Sin embargo, debe tener la seguridad de que no está exponiendo un punto débil de la seguridad cada vez que lo hace.  
  
 La siguiente ilustración muestra el recorrido de la pila que se produce cuando un método del ensamblado A4 solicita que sus llamadores tengan el permiso P.  
  
 ![Seguridad de acceso del código](../../../docs/framework/misc/media/slide-10a.gif "slide_10a")  
Recorrido de la pila de seguridad  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Temas relacionados  
  
|Título|Descripción|  
|-----------|-----------------|  
|[Code Access Security Basics](../../../docs/framework/misc/code-access-security-basics.md) (Conceptos básicos sobre la seguridad de acceso del código)|Describe la seguridad de acceso del código y sus usos más comunes.|  
|[Código transparente en seguridad, nivel 2](../../../docs/framework/misc/security-transparent-code-level-2.md)|Describe el modelo de transparencia de seguridad en .NET Framework 4.|  
|[Utilizar bibliotecas de código que no es de plena confianza](../../../docs/framework/misc/using-libraries-from-partially-trusted-code.md)|Describe cómo habilitar bibliotecas para usarlas con código no administrado y cómo usar las bibliotecas desde el código no administrado.|  
|[Conceptos clave de seguridad](../../../docs/standard/security/key-security-concepts.md)|Proporciona información general sobre muchos de los términos y conceptos clave que se usan en el sistema de seguridad de .NET Framework.|  
|[Seguridad basada en roles](../../../docs/standard/security/role-based-security.md)|Describe cómo incorporar la seguridad basada en roles.|  
|[Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)|Describe cómo incorporar la criptografía en las aplicaciones.|
