---
title: 'Estrategia de seguridad de WPF: Seguridad de plataforma'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- platform security model [WPF]
- Common Language Runtime (CLR) security features
- operating system security model [WPF]
- Internet Explorer security features [WPF]
- Security-Critical method
- CLR security features [WPF]
- security model [WPF]
- security model [WPF], platform
- WPF [WPF], about security model
- Windows Presentation Foundation [WPF], about security model
- security model [WPF], operating system
ms.assetid: 2a39a054-3e2a-4659-bcb7-8bcea490ba31
ms.openlocfilehash: 5b40302d93ce1bfc378b86210ed7bb54732d294b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67756756"
---
# <a name="wpf-security-strategy---platform-security"></a>Estrategia de seguridad de WPF: Seguridad de plataforma
Aunque Windows Presentation Foundation (WPF) ofrece una variedad de servicios de seguridad, también aprovecha las características de seguridad de la plataforma subyacente, que incluye el sistema operativo, el [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)], y [!INCLUDE[TLA2#tla_ie](../../../includes/tla2sharptla-ie-md.md)]. Estas capas se combinan para proporcionar a [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] un modelo de seguridad sólido y profundo que intenta evitar todos los puntos flacos, como se muestra en la ilustración siguiente:  
  
 ![Diagrama que muestra el modelo de seguridad WPF.](./media/wpf-security-strategy-platform-security/windows-presentation-foundation-security.png)  
  
 En el resto de este tema se describen las características de cada una de estas capas que pertenecen específicamente a [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)].  

<a name="Operating_System_Security"></a>   
## <a name="operating-system-security"></a>Seguridad del sistema operativo  
 El nivel mínimo de sistema operativo requerido por [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] es [!INCLUDE[TLA2#tla_winxpsp2](../../../includes/tla2sharptla-winxpsp2-md.md)]. El núcleo de [!INCLUDE[TLA2#tla_winxpsp2](../../../includes/tla2sharptla-winxpsp2-md.md)] proporciona varias características de seguridad que forman la base de seguridad para todas las aplicaciones de Windows, incluidas aquellas creadas con [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]. [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)] incorpora las características de seguridad de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] y las amplía. En este tema se aborda el alcance de estas características de seguridad que son importantes para [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)], así como la integración de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] con ellas para ofrecer una mayor defensa en profundidad.  
  
<a name="Microsoft_Windows_XP_Service_Pack_2__SP2_"></a>   
### <a name="microsoft-windows-xp-service-pack-2-sp2"></a>Microsoft Windows XP Service Pack 2 (SP2)  
 Además de una revisión general y refuerzo de Windows, hay tres características clave de [!INCLUDE[TLA2#tla_winxpsp2](../../../includes/tla2sharptla-winxpsp2-md.md)] que trataremos en este tema:  
  
- Compilación /GS  
  
- [!INCLUDE[TLA#tla_win_update](../../../includes/tlasharptla-win-update-md.md)]  
  
#### <a name="gs-compilation"></a>Compilación /GS  
 [!INCLUDE[TLA2#tla_winxpsp2](../../../includes/tla2sharptla-winxpsp2-md.md)] proporciona protección mediante la recopilación de muchas bibliotecas de sistema principales, incluidas todas las dependencias de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] como el [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)], para ayudar a mitigar las saturaciones del búfer. Esto se logra usando el parámetro /GS con el compilador de línea de comandos de C o C++. Aunque las saturaciones del búfer se deben evitar de manera explícita, la compilación /GS proporciona un ejemplo de una defensa en profundidad contra posibles vulnerabilidades creadas por dichas saturaciones de forma accidental o malintencionada.  
  
 Históricamente, las saturaciones del búfer han sido la causa de muchas vulnerabilidades de seguridad de gran impacto. Una saturación del búfer se produce cuando un atacante aprovecha una vulnerabilidad de código que permite la inserción de código malintencionado que escribe más allá de los límites de un búfer. Esto permite a un atacante secuestrar el proceso en el que se ejecuta el código; para ello, se sobrescribe la dirección de retorno de una función para que se ejecute el código del atacante. El resultado es un código malintencionado que ejecuta código arbitrario con los mismos privilegios que el proceso atacado.  
  
 En un nivel alto, la marca del compilador /GS protege contra algunas saturaciones del búfer potenciales mediante la inserción de una cookie de seguridad especial que protege la dirección de retorno de una función que tiene búferes de cadena locales. Una vez que se devuelve una función, la cookie de seguridad se compara con su valor anterior. Si el valor cambia, puede deberse a una saturación del búfer y el proceso se detiene con una condición de error. Detener el proceso impide la ejecución de código potencialmente malintencionado. Consulte [/GS (comprobación de seguridad del búfer)](/cpp/build/reference/gs-buffer-security-check) para obtener más detalles.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] se compila con la marca /GS para agregar una capa más de defensa a las aplicaciones de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)].  
  
#### <a name="microsoft-windows-update-enhancements"></a>Mejoras de Microsoft Windows Update  
 [!INCLUDE[TLA#tla_win_update](../../../includes/tlasharptla-win-update-md.md)] también se mejoró en [!INCLUDE[TLA2#tla_winxpsp2](../../../includes/tla2sharptla-winxpsp2-md.md)] para simplificar el proceso de descarga e instalación de actualizaciones. Estos cambios mejoran significativamente la seguridad de clientes de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)], ya que sirven para asegurar que sus sistemas están actualizados, especialmente en lo que se refiere a las actualizaciones de seguridad.  
  
<a name="Windows_Vista"></a>   
### <a name="windows-vista"></a>Windows Vista  
 Los usuarios de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] en [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)] se beneficiarán de las mejoras de seguridad adicionales del sistema operativo, incluidos “Acceso de usuario con privilegios mínimos”, comprobaciones de integridad de código y aislamiento de privilegios.  
  
#### <a name="user-account-control-uac"></a>Control de cuentas de usuario [UAC]  
 Hoy en día, los usuarios de Windows tienden a ejecutar con privilegios de administrador porque muchas aplicaciones requieren para la instalación o ejecución o ambos. Ser capaz de escribir la configuración predeterminada de una aplicación en el Registro es un ejemplo.  
  
 La ejecución con privilegios de administrador en realidad significa que las aplicaciones se ejecutan a partir de procesos que tienen concedidos privilegios de administrador. El efecto de esto en la seguridad es que cualquier código malintencionado que secuestre un proceso que se ejecuta con privilegios de administrador heredará automáticamente esos privilegios, incluido el acceso a recursos críticos del sistema.  
  
 Una manera de protegerse frente a esta amenaza de seguridad es ejecutar las aplicaciones con los privilegios mínimos necesarios. Esto se conoce como el principio de privilegios mínimos y es una característica fundamental del sistema operativo [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)]. Esta característica se denomina Control de cuentas de usuario (UAC) y [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)] la usa de dos maneras distintas:  
  
- Para ejecutar la mayoría de las aplicaciones con privilegios UAC de forma predeterminada, incluso si el usuario es un administrador; solo las aplicaciones que necesitan privilegios de administrador se ejecutarán con privilegios de administrador. Para ejecutarse con privilegios de administrador, las aplicaciones deben marcarse explícitamente en su manifiesto de aplicación o como entrada en la directiva de seguridad.  
  
- Para proporcionar soluciones de compatibilidad como la virtualización. Por ejemplo, muchas aplicaciones intentan escribir en ubicaciones restringidas, como C:\Archivos de programa. Para las aplicaciones que se ejecutan con UAC, existe una ubicación por usuario alternativa que no requiere privilegios de administrador para escribir en ella. Para las aplicaciones que se ejecutan en UAC, UAC virtualiza C:\Archivos de programa para que las aplicaciones que crean estar escribiendo en esa ubicación, en realidad lo estén haciendo en la ubicación por usuario alternativa. Este tipo de trabajo de compatibilidad permite al sistema operativo ejecutar muchas aplicaciones que anteriormente no se podían ejecutar en UAC.  
  
#### <a name="code-integrity-checks"></a>Comprobaciones de integridad de código  
 [!INCLUDE[TLA#tla_longhorn](../../../includes/tlasharptla-longhorn-md.md)] incorpora comprobaciones más severas de integridad de código para evitar la inserción de código malintencionado en los archivos del sistema o en el kernel en tiempo de carga o de ejecución. Esto va más allá de la protección de archivos de sistema.  
  
<a name="Limited_Rights_Process_for_Browser_Hosted_Applications"></a>   
### <a name="limited-rights-process-for-browser-hosted-applications"></a>Proceso de derechos limitados para las aplicaciones hospedadas en explorador  
 Las aplicaciones de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] hospedadas en explorador se ejecutan en el espacio aislado de la zona de Internet. La integración de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] con [!INCLUDE[TLA#tla_ie](../../../includes/tlasharptla-ie-md.md)] amplía esta protección con compatibilidad adicional.  
  
#### <a name="internet-explorer-6-service-pack-2-and-internet-explorer-7-for-xp"></a>Internet Explorer 6 Service Pack 2 e Internet Explorer 7 para XP  
 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] aprovecha la seguridad del sistema operativo mediante la limitación de privilegios de procesos para [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../includes/tlasharptla-winfxwebappsharpplural-md.md)] a fin de lograr una mayor protección. Antes de que se inicie una aplicación de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] hospedada en explorador, el sistema operativo crea un proceso de host que quita los privilegios innecesarios del token del proceso. Entre los privilegios que se quitan están la capacidad de apagar el equipo del usuario, la carga de controladores y el acceso de lectura a todos los archivos del equipo.  
  
#### <a name="internet-explorer-7-for-vista"></a>Internet Explorer 7 para Vista  
 En [!INCLUDE[TLA#tla_ie7](../../../includes/tlasharptla-ie7-md.md)], las aplicaciones de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] se ejecutan en modo protegido. En concreto, las [!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)] se ejecutan con integridad de nivel intermedio.  
  
#### <a name="defense-in-depth-layer"></a>Capa de defensa en profundidad  
 Puesto que las [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../includes/tlasharptla-winfxwebappsharpplural-md.md)] suelen limitarse al espacio aislado establecido por el conjunto de permisos de zona de Internet, quitar estos privilegios no daña las [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../includes/tlasharptla-winfxwebappsharpplural-md.md)] desde una perspectiva de compatibilidad. En su lugar, se crea una capa adicional de defensa en profundidad; aunque una aplicación en espacio aislado sea capaz de vulnerar otras capas y secuestrar el proceso, el proceso solo tendrá privilegios limitados.  
  
 Consulte [mediante una cuenta de usuario con privilegios mínimos](https://docs.microsoft.com/previous-versions/tn-archive/cc700846%28v=technet.10%29).  
  
<a name="Common_Language_Runtime_Security"></a>   
## <a name="common-language-runtime-security"></a>Seguridad de Common Language Runtime  
 [!INCLUDE[TLA#tla_clr](../../../includes/tlasharptla-clr-md.md)] ofrece varias ventajas clave de seguridad que incluyen validación y comprobación, [!INCLUDE[TLA#tla_cas](../../../includes/tlasharptla-cas-md.md)] y la metodología de seguridad crítica.  
  
<a name="Validation_and_Verification"></a>   
### <a name="validation-and-verification"></a>Validación y comprobación  
 Para proporcionar aislamiento de ensamblados e integridad, [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] usa un proceso de validación. La validación de [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] garantiza que los ensamblados se aíslen mediante la validación de su formato de archivo portable ejecutable (PE) para las direcciones que apuntan fuera del ensamblado. La validación de [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] también corrobora la integridad de los metadatos que se insertan en un ensamblado.  
  
 Para garantizar la seguridad de tipos, evitar problemas de seguridad comunes (por ejemplo, las saturaciones del búfer) y habilitar el espacio aislado a través de aislamiento de subprocesos, [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] seguridad usa el concepto de comprobación.  
  
 Las aplicaciones administradas se compilan en Lenguaje Intermedio de Microsoft (MSIL). Cuando se ejecutan métodos en una aplicación administrada, su MSIL se compila en código nativo a través de la compilación Just-In-Time (JIT). La compilación JIT incluye un proceso de comprobación que aplica numerosas reglas de seguridad y solidez para impedir que el código realice las siguientes acciones:  
  
- Infringir contratos de tipo  
  
- Introducir saturaciones del búfer  
  
- Tener acceso descontrolado a la memoria  
  
 El código administrado que no cumple las reglas de comprobación no tiene permiso para ejecutarse, a menos que se considere código de confianza.  
  
 La ventaja de código comprobable es una razón de por qué [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] se basa en .NET Framework. En la medida en que se usa el código comprobable, se reduce en gran medida la posibilidad de aprovecharse de las posibles vulnerabilidades.  
  
<a name="Code_Access_Security"></a>   
### <a name="code-access-security"></a>Seguridad de acceso del código  
 Una máquina cliente exhibe una amplia variedad de recursos a los que puede tener acceso una aplicación administrada, incluido el sistema de archivos, el Registro, los servicios de impresión, la interfaz de usuario, la reflexión y las variables de entorno. Antes de que una aplicación administrada puede tener acceso a cualquiera de los recursos en un equipo cliente, debe tener permiso de .NET Framework para hacerlo. Un permiso en [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] es una subclase de la <xref:System.Security.CodeAccessPermission>; [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] implementa una subclase para cada recurso al que pueden tener acceso las aplicaciones administradas.  
  
 Los permisos que [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] concede a una aplicación administrada cuando comienza a ejecutarse se conocen como conjunto de permisos y están determinados por la evidencia proporcionada por la aplicación. Para las aplicaciones de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)], la evidencia proporcionada es la ubicación —o zona— desde la que se inician las aplicaciones. [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] identifica las zonas siguientes:  
  
- **Mi PC**. Aplicaciones iniciadas desde la máquina cliente (de plena confianza).  
  
- **Intranet local**. Aplicaciones iniciadas desde la intranet (de confianza parcial).  
  
- **Internet**. Aplicaciones iniciadas desde Internet (de confianza mínima).  
  
- **Sitios de confianza**. Aplicaciones identificadas por un usuario como de confianza (de confianza mínima).  
  
- **Sitios que no son de confianza**. Aplicaciones identificadas por un usuario como no confiables (no confiables).  
  
 Para cada una de estas zonas, [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] proporciona un conjunto de permisos predefinidos que incluye los permisos que coinciden con el nivel de confianza asociado a cada una. Entre ellas se incluyen las siguientes:  
  
- **FullTrust**. Para las aplicaciones iniciadas desde la **Mi PC** zona. Se conceden todos los permisos posibles.  
  
- **LocalIntranet**. Para las aplicaciones iniciadas desde la **Intranet Local** zona. Un subconjunto de los permisos se concede para proporcionar acceso moderado a los recursos de una máquina cliente, incluido almacenamiento aislado, acceso sin restricciones a la interfaz de usuario, cuadros de diálogo de archivos sin restricciones, reflexión limitada y acceso limitado a las variables de entorno. No se proporcionan permisos para los recursos críticos, como el Registro.  
  
- **Internet**. Para las aplicaciones iniciadas desde la **Internet** o **sitios de confianza** zona. Un subconjunto de los permisos se concede para proporcionar acceso limitado a los recursos de una máquina cliente, incluido almacenamiento aislado, apertura exclusiva de archivos e interfaz de usuario limitada. En esencia, este permiso establecido aísla las aplicaciones de la máquina cliente.  
  
 Aplicaciones identificadas como pertenecientes a la **sitios de confianza** zona les concede ningún permiso por [!INCLUDE[TLA2#tla_cas](../../../includes/tla2sharptla-cas-md.md)] en absoluto. Por lo tanto, no existe un conjunto de permisos predefinidos para ellas.  
  
 La ilustración siguiente muestra la relación entre las zonas, conjuntos de permisos, permisos y recursos:  
  
 ![Diagrama que muestra los conjuntos de permisos CAS.](./media/wpf-security-strategy-platform-security/code-access-security-permissions-relationship.png)  
  
 Las restricciones del recinto de seguridad de la zona de Internet se aplican igualmente a cualquier código que importa una aplicación XBAP desde una biblioteca del sistema, incluidos [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]. Esto garantiza que cada bit del código está bloqueado, incluso [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]. Desgraciadamente, para poder ejecutar una aplicación XBAP necesita ejecutar funcionalidades que necesitan más permisos que los habilitados por el recinto de seguridad de la zona de Internet.  
  
 Considere la posibilidad de una aplicación XBAP que incluye la siguiente página:  
  
 [!code-csharp[WPFPlatformSecuritySnippets#Permission](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFPlatformSecuritySnippets/CSharp/Page1.xaml.cs#permission)]
 [!code-vb[WPFPlatformSecuritySnippets#Permission](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFPlatformSecuritySnippets/VisualBasic/Page1.xaml.vb#permission)]  
  
 Para ejecutar esta aplicación XBAP, subyacente [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] código debe ejecutar más funcionalidades que está disponible para la aplicación XBAP que realiza la llamada, incluidos:  
  
- Creación de un identificador de ventana (HWND) para la representación  
  
- Envío de mensajes  
  
- Carga de la fuente Tahoma  
  
 Desde el un punto de vista de la seguridad, permitir el acceso directo a cualquiera de estas operaciones desde la aplicación en espacio aislado resultaría catastrófico.  
  
 Afortunadamente, [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] se encarga de esta situación ya que permite que estas operaciones se ejecuten con privilegios elevados en nombre de la aplicación en espacio aislado. Mientras que todos [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] operaciones se comprueban con los permisos limitados de seguridad de zona de Internet del dominio de aplicación de la aplicación XBAP, [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] (al igual que con otras bibliotecas de sistema) se concede un conjunto de permisos que incluye todos los permisos posibles.
  
 Esto requiere que [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] reciba privilegios elevados al tiempo que se evita que esos privilegios se rijan por el conjunto de permisos de zona de Internet del dominio de la aplicación host.  
  
 [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] lo consigue mediante la **Assert** método de un permiso. El siguiente código muestra cómo se produce esto:  
  
 [!code-csharp[WPFPlatformSecuritySnippets#Permission](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFPlatformSecuritySnippets/CSharp/Page1.xaml.cs#permission)]
 [!code-vb[WPFPlatformSecuritySnippets#Permission](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFPlatformSecuritySnippets/VisualBasic/Page1.xaml.vb#permission)]  
  
 El **Assert** esencialmente impide que los permisos ilimitados requeridos por [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] estén restringidos por Internet de la zona permisos de la aplicación XBAP.  
  
 Desde una perspectiva de plataforma, [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] es responsable de usar **Assert** correctamente; un uso incorrecto de **Assert** podría permitir que el código malintencionado elevase los privilegios. Por lo tanto, es importante sólo llamar a **Assert** cuando sea necesario, y para asegurarse de que sandbox restricciones permanecen intactas. Por ejemplo, el código en espacio aislado no tiene permiso para abrir archivos aleatorios, pero sí para usar fuentes. [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] permite que las aplicaciones en espacio aislado usar la funcionalidad de fuentes mediante una llamada a **Assert**y para [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] para leer los archivos que contienen estas fuentes en nombre de la aplicación en espacio aislado.  
  
<a name="ClickOnce_Deployment"></a>   
### <a name="clickonce-deployment"></a>implementación de ClickOnce  
 [!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)] es una tecnología de implementación completa que se incluye con .NET Framework y se integra con [!INCLUDE[TLA#tla_visualstu](../../../includes/tlasharptla-visualstu-md.md)] (consulte [ClickOnce seguridad e implementación](/visualstudio/deployment/clickonce-security-and-deployment) para obtener información detallada). Mientras que las aplicaciones independientes de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] pueden implementarse de forma optativa con [!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)], las aplicaciones hospedadas en explorador deben implementarse obligatoriamente con [!INCLUDE[TLA2#tla_clickonce](../../../includes/tla2sharptla-clickonce-md.md)].  
  
 Las aplicaciones implementadas mediante [!INCLUDE[TLA2#tla_clickonce](../../../includes/tla2sharptla-clickonce-md.md)] tienen una capa de seguridad adicional sobre [!INCLUDE[TLA#tla_cas](../../../includes/tlasharptla-cas-md.md)]; básicamente, las aplicaciones implementadas de [!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)] solicitan los permisos que necesitan. Esos permisos se les conceden únicamente si no exceden el conjunto de permisos para la zona desde la que se implementa la aplicación. Al reducir el conjunto de permisos a solo aquellos que sean necesarios, incluso si son menores que las proporcionadas por el permiso de la zona de inicio establecido, el número de recursos que la aplicación tiene acceso a se reduce al mínimo. Por lo tanto, si se secuestra la aplicación, se reduce la posibilidad de daños en la máquina cliente.  
  
<a name="Security_Critical_Methodology"></a>   
### <a name="security-critical-methodology"></a>Metodología crítica para la seguridad  
 El [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] código que usa permisos para habilitar el espacio aislado de zona de Internet para las aplicaciones XBAP se deben mantener en el máximo nivel de auditoría de seguridad y control. Para facilitar este requisito, .NET Framework proporciona nueva compatibilidad para administrar el código que eleva los privilegios. En concreto, el [!INCLUDE[TLA2#tla_clr](../../../includes/tla2sharptla-clr-md.md)] le permite identificar el código que eleva los privilegios y marcarlo con el <xref:System.Security.SecurityCriticalAttribute>; cualquier código no marcado con <xref:System.Security.SecurityCriticalAttribute> se convierte en *transparente* mediante esta metodología. Por el contrario, se impide que el código administrado que no está marcado con <xref:System.Security.SecurityCriticalAttribute> eleve sus privilegios.  
  
 La metodología de seguridad crítica permite la organización de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] código que eleva los privilegios en *kernel crítico para la seguridad*, con el resto sean transparente. Aislar el código crítico para la seguridad permite la [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] equipo de ingeniería centrar un control de origen y análisis de seguridad adicional en el kernel crítico para la seguridad más allá de las prácticas de seguridad estándar (vea [estrategia de seguridad de WPF -Ingeniería de seguridad](wpf-security-strategy-security-engineering.md)).  
  
 Tenga en cuenta que .NET Framework permite que el código de confianza para ampliar el espacio aislado de zona de Internet de XBAP, ya que permite a los desarrolladores escribir ensamblados administrados marcados con <xref:System.Security.AllowPartiallyTrustedCallersAttribute> (APTCA) e implementado del caché de ensamblados Global (GAC) para el usuario. Marcar un ensamblado con APTCA es una operación de seguridad muy sensible ya que permite que cualquier código llame a ese ensamblado, incluso el código malintencionado procedente de Internet. Cuando lo haga, extreme las precauciones y siga los procedimientos recomendados; asimismo, los usuarios deben confiar en el software para que pueda instalarse.  
  
<a name="Microsoft_Internet_Explorer_Security"></a>   
## <a name="microsoft-internet-explorer-security"></a>Seguridad de Microsoft Internet Explorer  
 Más allá de reducir los problemas de seguridad y simplificar la configuración de seguridad, [!INCLUDE[TLA#tla_ie6sp2](../../../includes/tlasharptla-ie6sp2-md.md)] contiene varias características que mejoran la seguridad para los usuarios de [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../includes/tlasharptla-winfxwebappsharpplural-md.md)]. Estas características intentan ofrecer a los usuarios un mayor control sobre su experiencia de exploración.  
  
 En versiones previas a [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)], los usuarios podían experimentar lo siguiente:  
  
- Ventanas emergentes aleatorias.  
  
- Redirección de script confusa.  
  
- Numerosos cuadros de diálogo de seguridad en algunos sitios web.  
  
 En algunos casos, sitios web de poca confianza trataban de engañar a los usuarios mediante la suplantación de la instalación de [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] o mostrando repetidamente un cuadro de diálogo de instalación de [!INCLUDE[TLA#tla_actx](../../../includes/tlasharptla-actx-md.md)], incluso después de que el usuario lo cancelase. Es posible que estas técnicas indujeran a un número significativo de usuarios a tomar malas decisiones que hayan dado lugar a la instalación de aplicaciones de spyware.  
  
 [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)] incluye varias características para mitigar este tipo de problemas centradas en el concepto de inicio por usuario. [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)] detecta cuándo un usuario hace clic en un vínculo o elemento de página antes de una acción, que se conoce como *inicio por usuario*, tratándolo de manera diferente a cuando una acción parecida se activa por la secuencia de comandos en una página. Por ejemplo, [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)] incorpora un **Bloqueador de elementos emergentes** que detecta si un usuario hace clic en un botón antes de la página de creación de una ventana emergente. De este modo, [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)] permite la mayoría de los elementos emergentes inocuos y evita los elementos emergentes que los usuarios no solicitan ni desean. Los elementos emergentes bloqueados se capturan en la nueva **barra de información**, que permite al usuario invalidar manualmente el bloqueo y ver la ventana emergente.  
  
 También se aplica la misma lógica de iniciación por usuario a **abierto**/**guardar** las advertencias de seguridad. Los cuadros de diálogo de instalación de [!INCLUDE[TLA2#tla_actx](../../../includes/tla2sharptla-actx-md.md)] siempre se capturan en la Barra de información, a menos que representen una actualización de un control previamente instalado. Estas medidas se combinan para brindar a los usuarios una experiencia de usuario más segura y controlada, puesto que están protegidos contra los sitios que les importunan para instalar software malintencionado o no deseado.  
  
 Estas características también protegen a los clientes que usan [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)] para ir a sitios web donde pueden descargar e instalar las aplicaciones de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]. En concreto, esto se debe a que [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)] ofrece una mejor experiencia de usuario que reduce la posibilidad de que los usuarios instalen aplicaciones malintencionadas o dañinas independientemente de qué tecnología se utilizó para crearlas, incluido [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)]. [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] se suma a estas protecciones usando [!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)] para facilitar la descarga de sus aplicaciones a través de Internet. Puesto que las [!INCLUDE[TLA#tla_winfxwebapp#plural](../../../includes/tlasharptla-winfxwebappsharpplural-md.md)] se ejecutan dentro de un espacio aislado de seguridad de la zona de Internet, pueden iniciarse sin problemas. Por otro lado, las aplicaciones de [!INCLUDE[TLA2#tla_wpf](../../../includes/tla2sharptla-wpf-md.md)] independientes requieren plena confianza para ejecutarse. Para estas aplicaciones, [!INCLUDE[TLA#tla_clickonce](../../../includes/tlasharptla-clickonce-md.md)] mostrará un cuadro de diálogo de seguridad durante el proceso de inicio a fin de notificar el uso de los requisitos de seguridad adicionales de la aplicación. Sin embargo, esto debe ser iniciado por el usuario, se regirá por la lógica iniciada por el usuario y se puede cancelar.  
  
 [!INCLUDE[TLA2#tla_ie7](../../../includes/tla2sharptla-ie7-md.md)] incorpora y amplía las capacidades de seguridad de [!INCLUDE[TLA2#tla_ie6sp2](../../../includes/tla2sharptla-ie6sp2-md.md)] como parte de un compromiso continuo con la seguridad.  
  
## <a name="see-also"></a>Vea también

- [Seguridad de acceso del código](../misc/code-access-security.md)
- [Seguridad](security-wpf.md)
- [Seguridad de confianza parcial de WPF](wpf-partial-trust-security.md)
- [Estrategia de seguridad de WPF: Ingeniería de seguridad](wpf-security-strategy-security-engineering.md)
