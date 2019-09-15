---
title: Cómo depurar servicios y aplicaciones con reconocimiento de notificaciones mediante el seguimiento de WIF
ms.date: 03/30/2017
ms.assetid: 3d51ba59-3adb-4ca4-bd33-5027531af687
author: BrucePerlerMS
ms.openlocfilehash: 604ebf5ad71197f6614ffa45b6d7c181d474e1aa
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990478"
---
# <a name="how-to-debug-claims-aware-applications-and-services-using-wif-tracing"></a>Cómo depurar servicios y aplicaciones con reconocimiento de notificaciones mediante el seguimiento de WIF
## <a name="applies-to"></a>Se aplica a  
  
- Microsoft® Windows® Identity Foundation (WIF)  
  
- Herramienta del visor de seguimiento de servicio (SvcTraceViewer.exe)  
  
- Solución de problemas y depuración de aplicaciones de WIF  
  
## <a name="summary"></a>Resumen  
 En este procedimiento se describen los pasos necesarios para configurar el seguimiento de WIF, recopilar registros de seguimiento y analizar los registros de seguimiento con la herramienta Visor de seguimiento. Proporciona una correspondencia entre las entradas de seguimiento y las acciones necesarias para solucionar los problemas relacionados con WIF.  
  
## <a name="contents"></a>Contenido  
  
- Objetivos  
  
- Resumen de pasos  
  
- Paso 1: configurar el seguimiento de WIF mediante el archivo de configuración Web.config  
  
- Paso 2: analizar los archivos de seguimiento de WIF mediante la herramienta Visor de seguimiento  
  
- Paso 3: identificar soluciones para corregir los problemas relacionados con WIF  
  
- Elementos relacionados  
  
## <a name="objectives"></a>Objetivos  
  
- Configurar el seguimiento de WIF.  
  
- Ver los registros de seguimiento en la herramienta Visor de seguimiento.  
  
- Identificar los problemas relacionados con WIF en los registros de seguimiento.  
  
- Aplicar acciones correctivas a los problemas relacionados con WIF encontrados en los registros de seguimiento.  
  
## <a name="summary-of-steps"></a>Resumen de pasos  
  
- Paso 1: configurar el seguimiento de WIF mediante el archivo de configuración Web.config  
  
- Paso 2: analizar los archivos de seguimiento de WIF mediante la herramienta Visor de seguimiento  
  
- Paso 3: identificar soluciones para corregir los problemas relacionados con WIF  
  
## <a name="step-1--configure-wif-tracing-using-webconfig-configuration-file"></a>Paso 1: configurar el seguimiento de WIF mediante el archivo de configuración Web.config  
 En este paso, realizará cambios en las secciones de configuración del archivo *Web.config* que permite a WIF realizar un seguimiento de sus eventos y almacenarlos en un registro de seguimiento.  
  
#### <a name="to-configure-wif-tracing-using-webconfig-configuration-file"></a>Para configurar el seguimiento de WIF mediante el archivo de configuración Web.config  
  
1. Abra el archivo de configuración raíz **Web.config** o **App.config** en el editor de Visual Studio. Para ello, haga doble clic en él en el **Explorador de soluciones**. Si su solución no tiene un archivo de configuración **Web.config** o **App.config**, agréguelo. Para ello, haga clic con el botón derecho en la solución en el **Explorador de soluciones**, haga clic en **Agregar** y, después, haga clic en **Nuevo elemento…** En el cuadro de diálogo **Nuevo elemento**, seleccione **Archivo de configuración de la aplicación** para **App.config** o **Archivo de configuración web** para **Web.config** en la lista y haga clic en **Aceptar**.  
  
2. Agregue las entradas de configuración similares a las siguientes al archivo de configuración, en el nodo **\<configuration>** al final del archivo de configuración:  
  
    ```xml  
    <system.diagnostics>  
        <sources>  
            <source name="System.IdentityModel" switchValue="Verbose">  
                <listeners>  
                    <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="WIFTrace.e2e"/>  
                </listeners>  
            </source>  
        </sources>  
        <trace autoflush="true"/>  
    </system.diagnostics>  
    ```  
  
3. La configuración anterior le indica a WIF que genere eventos de seguimiento detallados y los registre en el archivo *WIFTrace.e2e*. Para obtener una lista completa de los valores del modificador **switchValue** , consulte la tabla del nivel de seguimiento que se encuentra en el tema siguiente: [Configuración](../wcf/diagnostics/tracing/configuring-tracing.md)de la traza.  
  
## <a name="step-2--analyze-wif-trace-files-using-trace-viewer-tool"></a>Paso 2: analizar los archivos de seguimiento de WIF mediante la herramienta Visor de seguimiento  
 En este paso, usará la herramienta Visor de seguimiento (SvcTraceViewer.exe) para analizar los registros de seguimiento de WIF.  
  
#### <a name="to-analyze-wif-trace-logs-using-trace-viewer-tool-svctraceviewerexe"></a>Para analizar los registros de seguimiento de WIF con la herramienta Visor de seguimiento (SvcTraceViewer.exe)  
  
1. La herramienta Visor de seguimiento (SvcTraceViewer.exe) se incluye como parte de Windows SDK. Si aún no ha instalado el Windows SDK, puede descargarlo aquí: [Windows SDK](https://www.microsoft.com/download/en/details.aspx?id=8279).  
  
2. Ejecute la herramienta Visor de seguimiento (SvcTraceViewer.exe) Normalmente está disponible en la carpeta **Bin** de la ruta de instalación.  
  
3. Para abrir el archivo de registro de seguimiento de WIF, por ejemplo, WIFTrace.e2e, seleccione la opción **Archivo**, **Abrir…** en el menú o use el acceso directo **Ctrl+O**. Se abre el archivo de registro de seguimiento en la herramienta Visor de seguimiento.  
  
4. Consulte las entradas de la pestaña **Actividad**. Cada entrada debe contener un número de actividad, el número de seguimientos que se registraron, la duración de la actividad y sus marcas de tiempo de inicio y finalización.  
  
5. Haga clic en la pestaña **Actividad**. Verá las entradas de seguimiento detalladas en el área principal de la herramienta. Use la lista desplegable **nivel** del menú para filtrar el nivel específico de seguimientos, por ejemplo: **Todo**, **ADVERTENCIA**, **errores**, **información**, etc.  
  
6. Haga clic en entradas de seguimiento específicas para revisar los detalles en el área inferior de la herramienta. Elija las pestañas **Con formato** o **XML** para ver los detalles en la vista correspondiente.  
  
## <a name="step-3--identify-solutions-to-fix-wif-related-issues"></a>Paso 3: identificar soluciones para corregir los problemas relacionados con WIF  
 En este paso, puede encontrar soluciones a problemas relacionados con WIF identificados con la herramienta Visor de seguimiento y el registro de seguimiento de WIF. Realiza una correspondencia general entre las excepciones de WIF y sus posibles soluciones o las acciones necesarias para solucionar el problema.  
  
#### <a name="to-identify-solutions-to-fix-wif-related-issues"></a>Para identificar soluciones para corregir los problemas relacionados con WIF  
  
1. Revise la siguiente tabla de excepciones de WIF y las acciones necesarias para corregir los problemas.  
  
|**Identificador del error**|**Mensaje de error**|**Acción necesaria para corregir el error**|  
|-|-|-|  
|ID4175|IssuerNameRegistry no reconoció el emisor del token de seguridad.  Para aceptar los tokens de seguridad de este emisor, configure IssuerNameRegistry para devolver un nombre válido para este emisor.|Este error se puede producir cuando se copia una huella digital desde el complemento MMC y se pega en el archivo *Web.config*. En concreto, puede obtener un carácter adicional no imprimible en la cadena de texto cuando se copia desde la ventana de propiedades del certificado. Este carácter adicional produce un error en la coincidencia de la huella digital. El procedimiento para copiar correctamente la huella digital se puede encontrar en [el inicio de sesión único basado en notificaciones para web y Microsoft Azure](https://docs.microsoft.com/previous-versions/msp-n-p/ff359102%28v=pandp.10%29).|  
  
## <a name="related-items"></a>Elementos relacionados  
  
- [Uso del visor de seguimiento de servicios para ver seguimientos asociados y para la solución de problemas](../wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)
