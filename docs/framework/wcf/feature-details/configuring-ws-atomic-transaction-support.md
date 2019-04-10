---
title: Configuración de la compatibilidad con WS-Atomic Transaction
ms.date: 03/30/2017
helpviewer_keywords:
- WS-AT protocol [WCF], configuring WS-Atomic Transaction
ms.assetid: cb9f1c9c-1439-4172-b9bc-b01c3e09ac48
ms.openlocfilehash: 987d6c12262fd6530c6ef6f14cedeec269d3f2f8
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59315184"
---
# <a name="configuring-ws-atomic-transaction-support"></a>Configuración de la compatibilidad con WS-Atomic Transaction
En este tema se describe cómo puede configurar WS-AtomicTransaction (WS-AT) admiten utilizando la WS-AT Utilidad de configuración.  
  
## <a name="using-the-ws-at-configuration-utility"></a>Utilizar la utilidad de configuración WS-AT  
 La Utilidad de configuración WS-AT (wsatConfig.exe) se utiliza para configurar los valores WS-AT. Para permitir el servicio de protocolo WS-AT, debe utilizar la utilidad de configuración para configurar el puerto HTTPS para WS-AT, enlazar un certificado X.509 a los puertos HTTPS y configurar los certificados del socio autorizado especificando los nombres de sujeto o huellas digitales del certificado. La utilidad de configuración también le permite seleccionar el modo de la traza y salida predeterminada establecida y tiempos de espera de transacción entrante de máximo.  
  
 Puede tener acceso a la funcionalidad de esta herramienta utilizando un complemento de la página de propiedades Microsoft Management Console (MMC) de la consola de administración de los Servicios de componentes o desde una ventana de línea de comandos. Configure la compatibilidad WS-AT en el equipo local a través de la ventana de línea de comandos; configure los valores de los equipos locales y remotos utilizando el complemento MMC.  
  
 Se puede tener acceso a la ventana de línea de comandos en la ubicación de instalación de Windows SDK "%WINDIR%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation".  
  
 Para obtener más información acerca de la herramienta de línea de comandos, consulte [WS-AtomicTransaction Configuration Utility (wsatConfig.exe)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md).  
  
 Si está ejecutando [!INCLUDE[wxp](../../../../includes/wxp-md.md)] o [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], puede acceder el complemento MMC navegando a **Control Panel/Administrative Tools/servicios de componentes**, hacer clic **Mi PC**, y seleccionar **propiedades**. Ésta es la misma ubicación donde puede configurar Microsoft DTC (Coordinador de transacciones distribuidas). Las opciones disponibles para la configuración se agrupan bajo el **WS-AT** ficha. Si está ejecutando Windows Vista o [!INCLUDE[lserver](../../../../includes/lserver-md.md)], se encuentra el complemento de MMC, haga clic en el **iniciar** botón y escriba `dcomcnfg.exe` en el **búsqueda** cuadro. Cuando se abre la consola MMC, vaya a la **mi pc\coordinador de transacciones local DTC** nodo, haga clic y seleccione **propiedades**. Las opciones disponibles para la configuración se agrupan bajo el **WS-AT** ficha.  
  
 Para obtener más información sobre el complemento, vea la [complemento MMC de configuración de WS-AtomicTransaction](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md).  
  
 Para habilitar la interfaz de usuario de la herramienta, debe registrar primero el archivo WsatUI.dll, ubicado en la ruta de acceso siguiente  
  
 %PROGRAMFILES%\Microsoft SDKs\Windows\v6.0\Bin  
  
 Para registrar el producto, ejecute el comando siguiente en una ventana indicadora de Comando:  
  
 `regasm.exe /codebase WsatUI.dll`  
  
## <a name="enabling-ws-at"></a>Habilitar WS-AT  
 Para permitir el servicio de protocolo WS-AT dentro de MSDTC utilizando el puerto 443 y un certificado X.509 con una clave privada instalada en el almacén del equipo local, utilice la herramienta wsatConfig.exe con el comando siguiente.  
  
 `WsatConfig.exe –network:enable –port:8443 –endpointCert:<machine|"Issuer\SubjectName"> -accountsCerts:<thumbprint|"Issuer\SubjectName"> -restart`  
  
 Sustituya los parámetros respectivos con valores correspondientes a su entorno.  
  
 Para deshabilitar el servicio de protocolo WS-AT dentro de MSDTC, utilice la herramienta wsatConfig.exe con el comando siguiente.  
  
 `WsatConfig.exe –network:disable -restart`  
  
## <a name="configuring-trust-between-two-machines"></a>Configurar la confianza entre dos equipos  
 El servicio de protocolo WS-AT exige al administrador que autorice explícitamente las cuentas individuales a participar en transacciones distribuidas. Si es un administrador para dos equipos, puede configurar ambos equipos para establecer una relación de confianza mutua intercambiando el conjunto derecho de certificados entre los equipos, instalándolos en los almacenes de certificados adecuados y utilizando la herramienta wsatConfig.exe para agregar el certificado de cada equipo a la otra lista de certificados participantes autorizados. Este paso es necesario para realizar las transacciones distribuidas entre dos equipos mediante WS-AT.  
  
 En el ejemplo siguiente, se detallan los pasos para establecer la confianza entre dos equipos, A y B.  
  
### <a name="creating-and-exporting-certificates"></a>Crear y exportar Certificados  
 Este procedimiento requiere el Complemento de Certificados MMC. Se puede tener acceso al complemento abriendo el menú Inicio/Ejecutar, escribiendo "mmc" en el cuadro de entrada y presionando Aceptar. A continuación, en el **Consola1** ventana, vaya a **el archivo/agregar o quitar** complemento, haga clic en Agregar y elija **certificados** desde el **disponible de forma independiente Complementos** lista. Por último, seleccione **cuenta de equipo** para administrar y haga clic en **Aceptar**. El **certificados** nodo aparece en la consola de complemento.  
  
 En este momento, poseerá los certificados necesarios para establecer la confianza. Para obtener información sobre cómo crear e instalar nuevos certificados antes de los pasos siguientes, vea [Cómo: Crear e instalar certificados de cliente temporales en WCF durante el desarrollo](https://go.microsoft.com/fwlink/?LinkId=158925).  
  
1. En el equipo A, usando el complemento de los certificados MMC, importe el certificado existente (certA) en el almacén LocalMachine\MY (Nodo Personal) y LocalMachine\ROOT (nodo de entidad de certificación raíz de confianza). Para importar un certificado a un nodo específico, haga clic en el nodo y elija **todas las tareas/importar**.  
  
2. En el equipo B, usando el Complemento de certificados MMC, cree u obtenga el certificado certB con una clave privada e impórtelo a LocalMachine\MY (Nodo Personal) y al almacén LocalMachine\ROOT (nodo entidad de certificación raíz de confianza).  
  
3. Exporte la clave pública de certA a un archivo si aún no lo ha hecho.  
  
4. Exporte la clave pública de certB a un archivo si aún lo ha hecho.  
  
### <a name="establishing-mutual-trust-between-machines"></a>Establecer la confianza mutua entre los equipos  
  
1. En el equipo A, importe la representación del archivo de certB a los almacenes LocalMachine\ROOT y LocalMachine\MY. Esto declara que la máquina A confía en el certB para comunicarse con él.  
  
2. En el equipo B, importe el archivo certA en los almacenes LocalMachine\ROOT y LocalMachine\MY. Esto implica que el equipo B confía en el certA para comunicarse con él.  
  
 Después de completar estos pasos, se establece la confianza entre los dos equipos y se pueden configurar para comunicarse entre ellos mediante WS-AT.  
  
### <a name="configuring-msdtc-to-use-certificates"></a>Configurar MSDTC para utilizar certificados  
 Desde que el servicio de protocolo WS-AT actúa como un cliente y un servidor, debe realizar escuchas para las conexiones entrantes e iniciar las conexiones de salida. Por consiguiente, necesita configurar MSDTC para que sepa qué certificado utilizar al comunicarse con partes externas y qué certificados autorizar al aceptar la comunicación de entrada.  
  
 Puede configurarlo mediante el complemento WS-AT de MMC. Para obtener más información sobre esta herramienta, consulte el [complemento MMC de configuración de WS-AtomicTransaction](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md) tema. Los pasos siguientes describen cómo establecer la confianza entre dos equipos que ejecutan MSDTC.  
  
1. Configure los valores de la máquina A. Para "Certificado de punto de conexión", seleccione certA. Para "Certificados autorizados", seleccione certB.  
  
2. Configure los valores de la máquina B. Para "Certificado de punto de conexión", seleccione certB. Para "Certificados autorizados", seleccione certA.  
  
> [!NOTE]
>  Cuando una máquina envía un mensaje a otra máquina, el remitente intenta comprobar que el nombre de sujeto del certificado del destinatario y el nombre de la máquina del destinatario coinciden. Si no coinciden, se produce un error en la comprobación del certificado y las dos máquinas no se pueden comunicar.  
>   
>  Para un equipo unido a un dominio, el nombre es el nombre de dominio completo. De forma predeterminada, el nombre de un equipo en un grupo de trabajo es el nombre NetBIOS del equipo. Sin embargo, el nombre también puede incluir un sufijo DNS (Sistema de nombres de dominio) si hay uno presente en la conexión usada entre las dos máquinas.  
>   
>  Si el nombre del equipo cambia, por ejemplo, si un equipo del grupo de trabajo se une a un dominio, debe reeditar los certificados o configurar manualmente los sufijos DNS.  
  
## <a name="security"></a>Seguridad  
 Puesto que algunos de los valores relacionados con MSDTC y WS-AT están almacenados en el registro en HKLM\Software\Microsoft\MSDTC y en HKLM\Software\Microsoft\WSAT, respectivamente, asegúrese de que estas claves del Registro están protegidas para que solamente puedan escribir los administradores. En la herramienta Editor del registro, haga clic en la clave que desea proteger y seleccione **permiso** para establecer el control de acceso adecuado. Es importante para la seguridad e integridad del sistema que las claves importantes sean de solo lectura para los usuarios con pocos privilegios.  
  
 Al implementar MSDTC, el administrador debe asegurarse de que los intercambios de datos de MSDTC son seguros. En una implementación del grupo de trabajo, aísle la infraestructura transaccional de usuarios malintencionados; en una implementación en clúster, proteja el registro del clúster.  
  
## <a name="tracing"></a>Traza  
 Admite el servicio de protocolo WS-AT integrado, transacciones traza específica que se puede habilitar y administrado mediante el uso de la [complemento MMC de configuración de WS-AtomicTransaction](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md) herramienta.  Los seguimientos pueden incluir datos que indican la hora en que se realiza una inscripción para una transacción específica, la hora en que una transacción llega a su estado terminal, el resultado que ha recibido cada inscripción de transacción. Todos los seguimientos se pueden ver mediante el [herramienta Service Trace Viewer (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) herramienta.  
  
 El protocolo de servicio WS-AT también admite traza ServiceModel integrada a través de la sesión de traza de ETW. Esto proporciona seguimientos más detallados, específicos de la comunicación, además de los seguimientos de transacción existentes.  Para habilitar estos seguimientos adicionales, siga estos pasos:  
  
1. Abra el **iniciar/ejecutar** menú, escriba "regedit" en el cuadro de entrada y seleccione **Aceptar**.  
  
2. En el **Editor del registro**, vaya a la siguiente carpeta en el panel izquierdo, Hkey_Local_Machine\SOFTWARE\Microsoft\WSAT\3.0\  
  
3. Haga clic en el `ServiceModelDiagnosticTracing` valor en el panel derecho y seleccione **modificar**.  
  
4. En el **datos del valor** cuadro de entrada, escriba uno de los siguientes valores válidos para especificar el nivel de seguimiento que desea habilitar.  
  
-   0: desactivado  
  
-   1: crítico  
  
-   3: error. Éste es el valor predeterminado.  
  
-   7: advertencia  
  
-   15: información  
  
-   31: detallado  
  
## <a name="see-also"></a>Vea también

- [Utilidad de configuración de WS-AtomicTransaction (wsatConfig.exe)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
- [Complemento MMC de configuración de WS-AtomicTransaction](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)
