---
title: Proveedor de pertenencia y roles
ms.date: 03/30/2017
ms.assetid: 0d11a31c-e75f-4fcf-9cf4-b7f26e056bcd
ms.openlocfilehash: b5cb743fb3533d2f3a8016c9357d6ead498a5878
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59768168"
---
# <a name="membership-and-role-provider"></a>Proveedor de pertenencia y roles
El ejemplo de proveedor de pertenencia y función muestra el modo en que un servicio puede utilizar los proveedores de pertenencia y función de [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] para autenticar y autorizar a los clientes.  
  
 En este ejemplo, el cliente es una aplicación de consola (.exe) y los Servicios de Internet Information Server (IIS) hospedan el servicio.  
  
> [!NOTE]
>  El procedimiento de instalación y las instrucciones de compilación de este ejemplo se encuentran al final de este tema.  
  
 Este ejemplo demuestra cómo:  
  
-   Un cliente se puede autenticar utilizando la combinación de nombre de usuario y contraseña.  
  
-   El servidor puede validar las credenciales del cliente con el proveedor de pertenencia de [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
-   El servidor se puede autenticar utilizando el certificado X.509 del servidor.  
  
-   El servidor puede asignar el cliente autenticado a un rol utilizando el proveedor de roles de [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].  
  
-   El servidor puede utilizar `PrincipalPermissionAttribute` para controlar el acceso a ciertos métodos expuestos por el servicio.  
  
 Los proveedores de roles y pertenencia se configuran para utilizar un almacén respaldado por SQL Server. En el archivo de configuración del servicio se especifica una cadena de conexión y varias opciones. Al proveedor de pertenencia se le da el nombre `SqlMembershipProvider` y al proveedor de roles se le da el nombre `SqlRoleProvider`.  
  
```xml  
<!-- Set the connection string for SQL Server -->  
<connectionStrings>  
  <add name="SqlConn"   
       connectionString="Data Source=localhost;Integrated Security=SSPI;Initial Catalog=aspnetdb;" />  
</connectionStrings>  
  
<system.web>  
  <!-- Configure the Sql Membership Provider -->  
  <membership defaultProvider="SqlMembershipProvider" userIsOnlineTimeWindow="15">  
    <providers>  
      <clear />  
      <add   
        name="SqlMembershipProvider"   
        type="System.Web.Security.SqlMembershipProvider"   
        connectionStringName="SqlConn"  
        applicationName="MembershipAndRoleProviderSample"  
        enablePasswordRetrieval="false"  
        enablePasswordReset="false"  
        requiresQuestionAndAnswer="false"  
        requiresUniqueEmail="true"  
        passwordFormat="Hashed" />  
    </providers>  
  </membership>  
  
  <!-- Configure the Sql Role Provider -->  
  <roleManager enabled ="true"   
               defaultProvider ="SqlRoleProvider" >  
    <providers>  
      <add name ="SqlRoleProvider"   
           type="System.Web.Security.SqlRoleProvider"   
           connectionStringName="SqlConn"   
           applicationName="MembershipAndRoleProviderSample"/>  
    </providers>  
  </roleManager>  
</system.web>  
```  
  
 El servicio expone un extremo único para comunicarse con el servicio, que se define utilizando el archivo de configuración Web.config. El punto de conexión está compuesto por una dirección, un enlace y un contrato. El enlace se configura con un `wsHttpBinding` estándar, que usa la autenticación de Windows de forma predeterminada. Este ejemplo establece el `wsHttpBinding` estándar para utilizar la autenticación mediante el nombre de usuario. El comportamiento especifica que se va a usar el certificado de servidor para la autenticación del servicio. El certificado de servidor debe contener el mismo valor para el `SubjectName` como el `findValue` atributo en el [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) elemento de configuración. Además, el comportamiento especifica que el proveedor de pertenencia de [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] realiza la autenticación de los pares nombre de usuario y contraseña, y que el proveedor de función de [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] realiza la asignación de funciones mediante la especificación de los nombres definidos para los dos proveedores.  
  
```xml  
<system.serviceModel>  
  
  <protocolMapping>  
    <add scheme="http" binding="wsHttpBinding" />  
  </protocolMapping>  
  
  <bindings>  
    <wsHttpBinding>  
      <!-- Set up a binding that uses Username as the client credential type -->  
      <binding>  
        <security mode ="Message">  
          <message clientCredentialType ="UserName"/>  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
  
  <behaviors>  
    <serviceBehaviors>  
      <behavior>  
        <!-- Configure role based authorization to use the Role Provider -->  
        <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                              roleProviderName ="SqlRoleProvider" />  
        <serviceCredentials>  
          <!-- Configure user name authentication to use the Membership Provider -->  
          <userNameAuthentication userNamePasswordValidationMode ="MembershipProvider"   
                                  membershipProviderName ="SqlMembershipProvider"/>  
          <!-- Configure the service certificate -->  
          <serviceCertificate storeLocation ="LocalMachine"   
                              storeName ="My"   
                              x509FindType ="FindBySubjectName"  
                              findValue ="localhost" />  
        </serviceCredentials>  
        <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
        <serviceDebug includeExceptionDetailInFaults="false" />  
        <serviceMetadata httpGetEnabled="true"/>  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
 Al ejecutar el ejemplo, el cliente llama a varias operaciones de servicio en tres distintas cuentas de usuario: Alice, Bob y Charlie. Las solicitudes y respuestas de la operación se muestran en la ventana de la consola del cliente. Las cuatro llamadas que se efectúan como el usuario "Alice" deberían poder realizarse correctamente. El usuario "Bob" debería obtener un error de acceso denegado al intentar llamar al método Divide. El usuario "Charlie" debería obtener un error de acceso denegado al intentar llamar al método Multiply. Presione ENTRAR en la ventana de cliente para cerrar el cliente.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Configurar, compilar y ejecutar el ejemplo  
  
1. Para compilar la edición de la solución de C# o Visual Basic. NET, siga las instrucciones de [ejecutando los ejemplos de Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
2. Asegúrese de que ha configurado el [ASP.NET Application Services Database](https://go.microsoft.com/fwlink/?LinkId=94997).  
  
    > [!NOTE]
    >  Si está ejecutando SQL Server Express Edition, su nombre de servidor es .\SQLEXPRESS. Se debería utilizar este servidor al configurar la base de datos de los servicios de aplicación de [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)], así como en la cadena de conexión de Web.config.  
  
    > [!NOTE]
    >  La cuenta de proceso de trabajo de [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] debe tener permisos en la base de datos que se crea en este paso. Use la utilidad sqlcmd o SQL Server Management Studio para ello.  
  
3. Para ejecutar el ejemplo en una configuración de equipos única o cruzada, utilice las instrucciones siguientes.  
  
### <a name="to-run-the-sample-on-the-same-computer"></a>Para ejecutar el ejemplo en el mismo equipo  
  
1. Asegúrese de que la ruta de acceso incluye la carpeta donde se encuentra Makecert.exe.  
  
2. Ejecute Setup.bat desde la carpeta de instalación de ejemplo en un símbolo del sistema de desarrollador de Visual Studio que se ejecute con privilegios de administrador. De esta forma se instalan los certificados de servicio necesarios para ejecutar el ejemplo.  
  
3. Inicie Client.exe desde \client\bin. La actividad del cliente se muestra en la aplicación de consola del cliente.  
  
4. Si el cliente y el servicio no se pueden comunicar, vea [sugerencias de solución de problemas para obtener ejemplos de WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
### <a name="to-run-the-sample-across-computers"></a>Para ejecutar el ejemplo en varios equipos  
  
1. Cree un directorio en el equipo del servicio. Cree una aplicación virtual denominada "servicemodelsamples" para este directorio utilizando la herramienta de administración de Internet Information Services (IIS).  
  
2. Copie los archivos de programa de servicio del directorio \inetpub\wwwroot\servicemodelsamples al directorio virtual del equipo de servicio. Asegúrese de que copia los archivos en el subdirectorio \bin. Copie también los archivos Setup.bat, GetComputerName.vbs y Cleanup.bat en el equipo de servicio.  
  
3. Cree un directorio en el equipo cliente para los archivos binarios del cliente.  
  
4. Copie los archivos de programa del cliente en el directorio del cliente en el equipo cliente. Copie también los archivos Setup.bat, Cleanup.bat e ImportServiceCert.bat en el cliente.  
  
5. En el servidor, abra un símbolo del sistema para desarrolladores de Visual Studio con privilegios administrativos y ejecute `setup.bat service`. Ejecutando `setup.bat` con el `service` argumento crea un certificado de servicio con el nombre de dominio completo del equipo y exporta el certificado de servicio a un archivo denominado Service.cer.  
  
6. Edite el archivo Web.config para reflejar el nuevo nombre del certificado (en el `findValue` atributo en el [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)), que es el mismo que el nombre de dominio completo del equipo.  
  
7. Copie el archivo Service.cer del directorio de servicio al directorio del cliente en el equipo cliente.  
  
8. En el archivo Client.exe.config del equipo cliente, cambie el valor de la dirección del punto de conexión para que coincida con la nueva dirección de su servicio.  
  
9. En el cliente, abra un símbolo del sistema para desarrolladores de Visual Studio con privilegios administrativos y ejecute ImportServiceCert.bat. Así se importa el certificado del servicio del archivo Service.cer en el almacén CurrentUser - TrustedPeople.  
  
10. En el equipo cliente, inicie Client.exe desde un símbolo del sistema. Si el cliente y el servicio no se pueden comunicar, vea [sugerencias de solución de problemas para obtener ejemplos de WCF](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90)).  
  
### <a name="to-clean-up-after-the-sample"></a>Para realizar una limpieza después de ejecutar el ejemplo  
  
-   Ejecute Cleanup.bat en la carpeta de ejemplos después de que haya terminado de ejecutar el ejemplo.  
  
> [!NOTE]
>  Este script no quita los certificados del servicio en un cliente cuando el ejemplo se ejecuta en varios equipos. Si ha ejecutado los ejemplos de Windows Communication Foundation (WCF) que usan certificados en varios equipos, asegúrese de borrar los certificados de servicio que se han instalado en el almacén CurrentUser - trustedpeople. Para ello, use el siguiente comando: `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>` Por ejemplo: `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`.  
  
## <a name="the-setup-batch-file"></a>Archivo de instalación por lotes  
 El archivo por lotes Setup.bat incluido con este ejemplo permite configurar el servidor con los certificados pertinentes para ejecutar una aplicación autohospedada que requiera seguridad basada en el certificado del servidor. Este archivo por lotes debe modificarse para que funcione en varios equipos o en un escenario sin hospedaje.  
  
 A continuación, se proporciona una breve descripción de las diferentes secciones de los archivos por lotes de manera que se puedan modificar para ejecutarse con la configuración adecuada.  
  
-   Crear el certificado de servidor.  
  
     Las líneas siguientes del archivo por lotes Setup.bat crean el certificado de servidor que se va a usar. La variable %SERVER_NAME% especifica el nombre del servidor. Cambie esta variable para especificar su propio nombre de servidor. Este archivo por lotes tiene como valor predeterminado el host local.  
  
     El certificado se almacena en el almacén My (Personal), en la ubicación de almacenamiento LocalMachine.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
-   Instalar el certificado del servidor en el almacén de certificados de confianza del cliente.  
  
     Las líneas siguientes del archivo por lotes Setup.bat copian el certificado de servidor en el almacén de los usuarios de confianza del cliente. Este paso es necesario porque el sistema cliente no confía implícitamente en los certificados generados por Makecert.exe. Si ya tiene un certificado que se basa en un certificado raíz de confianza del cliente, por ejemplo, un certificado emitido por Microsoft, no es necesario el paso de rellenar el almacén del certificado de cliente con el certificado de servidor.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
