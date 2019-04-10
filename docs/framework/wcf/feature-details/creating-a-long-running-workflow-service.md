---
title: Crear un servicio de flujo de trabajo de larga ejecución
ms.date: 03/30/2017
ms.assetid: 4c39bd04-5b8a-4562-a343-2c63c2821345
ms.openlocfilehash: ac0cb83ad428ce98a05fd0626fff835162ad0e41
ms.sourcegitcommit: 558d78d2a68acd4c95ef23231c8b4e4c7bac3902
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/09/2019
ms.locfileid: "59301352"
---
# <a name="creating-a-long-running-workflow-service"></a>Crear un servicio de flujo de trabajo de larga ejecución
En este tema se describe cómo crear un servicio de flujo de trabajo de larga ejecución. Los servicios de flujo de trabajo de larga ejecución se pueden ejecutar durante períodos de tiempo prolongados. En algún momento, el flujo de trabajo se puede inactivar a la espera de recibir información adicional. En este caso, el flujo de trabajo se conserva en una base de datos SQL y se quita de la memoria. Cuando esté disponible la información adicional, la instancia de flujo de trabajo se vuelve a cargar en la memoria y continua ejecutándose.  En este escenario, el usuario implementa un sistema de pedidos muy simplificado.  El cliente envía un mensaje inicial al servicio de flujo de trabajo para que inicie el pedido. Devuelve un identificador de pedido al cliente. En este momento el servicio de flujo de trabajo espera otro mensaje del cliente y pasa al estado inactivo, y se conserva en una base de datos SQL Server.  Cuando el cliente envía el siguiente mensaje para pedir un elemento, el servicio de flujo de trabajo se vuelve a cargar en memoria y finaliza el procesamiento del pedido. En el ejemplo de código devuelve una cadena que indica que el elemento se ha agregado al pedido. No se pretende que el ejemplo de código sea una aplicación real de la tecnología, sino más bien un ejemplo sencillo que ilustre servicios de flujo de trabajo de ejecución prolongada. En este tema se supone que sabe cómo crear soluciones y proyectos de Visual Studio 2012.

## <a name="prerequisites"></a>Requisitos previos
 Debe tener instalado el siguiente software para usar este tutorial:

1. Microsoft SQL Server 2008

2. Visual Studio 2012

3. Microsoft  [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]

4. Está familiarizado con WCF y Visual Studio 2012 y sabe cómo crear proyectos y soluciones.

### <a name="to-setup-the-sql-database"></a>Para configurar la base de datos SQL

1. Para conservar las instancias del servicio de flujo de trabajo debe tener instalado Microsoft SQL Server y configurar una base de datos con el fin de almacenar las instancias de flujo de trabajo persistentes. Ejecute Microsoft SQL Management Studio, haga clic en el **iniciar** button, seleccionar **todos los programas**, **Microsoft SQL Server 2008**, y **Microsoft SQL Management Studio**.

2. Haga clic en el **Connect** botón para iniciar sesión en la instancia de SQL Server

3. Haga clic en **bases de datos** en la vista de árbol y seleccione **nueva base de datos...** Para crear una base de datos nueva denominada `SQLPersistenceStore`.

4. Ejecute el archivo de script SqlWorkflowInstanceStoreSchema.sql ubicado en el directorio C:\Windows\Microsoft.NET\Framework\v4.0\SQL\es en la base de datos SQLPersistenceStore para configurar los esquemas de base de datos necesarios.

5. Ejecute el archivo de script SqlWorkflowInstanceStoreLogic.sql ubicado en el directorio C:\Windows\Microsoft.NET\Framework\v4.0\SQL\es en la base de datos SQLPersistenceStore para configurar la lógica de base de datos necesaria.

### <a name="to-create-the-web-hosted-workflow-service"></a>Para crear el servicio de flujo de trabajo hospedado en web

1. Crear una solución de Visual Studio 2012 vacía, asígnele el nombre `OrderProcessing`.

2. Agregue un nuevo proyecto de aplicación de servicio de flujo de trabajo WCF denominado `OrderService` a la solución.

3. En el cuadro de diálogo de propiedades de proyecto, seleccione el **Web** ficha.

    1.  En **acción de inicio** seleccione **página específica** y especifique `Service1.xamlx`.

         ![Propiedades de Web del proyecto de servicio de flujo de trabajo](./media/creating-a-long-running-workflow-service/start-action-specific-page-option.png "crear el servicio de flujo de trabajo hospedados en web - opción de página específica")

    2.  En **servidores** seleccione **servidor Web de IIS Local Use**.

         ![Configuración del servidor Web local](./media/creating-a-long-running-workflow-service/use-local-web-server.png "crear el servicio de flujo de trabajo hospedados en web - opción de usar servidor Web de IIS Local")

        > [!WARNING]
        >  Debe ejecutar Visual Studio 2012 en modo de administrador para poder realizar esta configuración.

         Estos dos pasos configuran el proyecto de servicio de flujo de trabajo que IIS va a hospedar.

4. Abra `Service1.xamlx` si está abierto aún no y eliminar las existentes **ReceiveRequest** y **SendResponse** actividades.

5. Seleccione el **servicio secuencial** actividad y haga clic en el **Variables** vincular y agregue las variables que se muestra en la siguiente ilustración. De esta forma, se agregan algunas variables que se usarán posteriormente en el servicio de flujo de trabajo.

    > [!NOTE]
    >  Si CorrelationHandle no está en la lista desplegable Tipo de Variable, seleccione **buscar tipos** en la lista desplegable. Escriba CorrelationHandle en el **nombre de tipo** , seleccione CorrelationHandle en el cuadro de lista y haga clic en **Aceptar**.

     ![Agregue Variables](./media/creating-a-long-running-workflow-service/add-variables-sequential-service-activity.gif "agregar variables a la actividad de servicio secuencial.")

6. Arrastre y coloque un **ReceiveAndSendReply** plantilla de actividad en el **servicio secuencial** actividad. Este conjunto de actividades recibirá un mensaje de un cliente y devolverá un respuesta.

    1.  Seleccione el **recepción** actividad y establezca las propiedades resaltadas en la siguiente ilustración.

         ![Establecer propiedades de actividad de recepción](./media/creating-a-long-running-workflow-service/set-receive-activity-properties.png "establecer las propiedades de la actividad de recepción.")

         La propiedad DisplayName establece el nombre mostrado para la actividad Receive en el diseñador. Las propiedades ServiceContractName y OperationName especifican el nombre del contrato de servicio y la operación que implementa la actividad Receive. Para obtener más información acerca de cómo se usan los contratos de servicios de flujo de trabajo, consulte [usar contratos en flujo de trabajo](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md).

    2.  Haga clic en el **definir...**  vincular en el **ReceiveStartOrder** actividad y establezca las propiedades que se muestra en la siguiente ilustración.  Tenga en cuenta que el **parámetros** botón de radio está seleccionado, un parámetro denominado `p_customerName` está enlazado a la `customerName` variable. Esto configura el **recepción** actividad para recibir algunos datos y enlazarlos a variables locales.

         ![Configuración de los datos recibidos por la actividad Receive](./media/creating-a-long-running-workflow-service/set-properties-for-receive-content.png "establecer las propiedades de los datos recibidos por la actividad Receive.")

    3.  Seleccione el **SendReplyToReceive** actividad y establezca la propiedad resaltada se muestra en la siguiente ilustración.

         ![Establecer las propiedades de la actividad SendReply](./media/creating-a-long-running-workflow-service/set-properties-for-reply-activities.png "SetReplyProperties")

    4.  Haga clic en el **definir...**  vincular en el **SendReplyToStartOrder** actividad y establezca las propiedades que se muestra en la siguiente ilustración. Tenga en cuenta que el **parámetros** botón de radio está seleccionado; un parámetro denominado `p_orderId` está enlazado a la `orderId` variable. Esta configuración especifica que la actividad SendReplyToStartOrder ejecutará un valor de tipo de cadena en el autor de la llamada.

         ![Configuración de los datos de contenido de actividad SendReply](./media/creating-a-long-running-workflow-service/setreplycontent-for-sendreplytostartorder-activity.png "configurar para la actividad SetReplyToStartOrder.")

    5.  Arrastre y coloque una actividad de asignación entre la **recepción** y **SendReply** actividades y establezca las propiedades tal como se muestra en la ilustración siguiente:

         ![Agregar una actividad de asignación](./media/creating-a-long-running-workflow-service/add-an-assign-activity.png "agregar una actividad de asignación.")

         De esta forma, se crea un identificador de nuevo pedido y se coloca el valor en la variable orderId.

    6.  Seleccione el **ReplyToStartOrder** actividad. En la ventana Propiedades, haga clic en el botón de puntos suspensivos para **CorrelationInitializers**. Seleccione el **agregar inicializador** vincular, escriba `orderIdHandle` en el cuadro de texto inicializador, seleccione el inicializador de correlación de consulta para el tipo de correlación y seleccione p_orderId en el cuadro de lista desplegable de las consultas XPATH. Esta configuración se muestra en la siguiente ilustración. Haga clic en **Aceptar**.  De esta forma, se inicializa una correlación entre el cliente y esta instancia del servicio de flujo de trabajo. Cuando se reciba un mensaje con este identificador de pedido, se enruta a esta instancia del servicio de flujo de trabajo.

         ![Agregar un inicializador de correlación](./media/creating-a-long-running-workflow-service/add-correlationinitializers.png "agregar un inicializador de correlación.")

7. Arrastre y coloque otra **ReceiveAndSendReply** actividad al final del flujo de trabajo (fuera de la **secuencia** que contiene la primera **recepción** y  **SendReply** actividades). De esta forma, se recibirá el segundo mensaje enviado por el cliente y se responderá al mismo.

    1.  Seleccione el **secuencia** que contiene el recién agregado **recepción** y **SendReply** actividades y haga clic en el **Variables** botón. Agregue la variable resaltada en la siguiente ilustración:

         ![Agregar nuevas variables](./media/creating-a-long-running-workflow-service/add-the-itemid-variable.png "agregue la variable ItemId.")

    2.  Seleccione el **recepción** actividad y establezca las propiedades que se muestra en la ilustración siguiente:

         ![Establecer las propiedades de la actividad de recepción](./media/creating-a-long-running-workflow-service/set-receive-activities-properties.png "establecer las propiedades de las actividades de recepción.")

    3.  Haga clic en el **definir...**  vincular en el **ReceiveAddItem** actividad y agregar los parámetros mostrados en la siguiente ilustración: Esto configura la actividad de recepción para Aceptar dos parámetros, el identificador de pedido y el identificador del elemento que se ordenan.

         ![Especificación de parámetros para la segunda recepción](./media/creating-a-long-running-workflow-service/add-receive-two-parameters.png "configurar la actividad de recepción para recibir dos parámetros.")

    4.  Haga clic en el **CorrelateOn** puntos suspensivos situado y escriba `orderIdHandle`. En **consultas XPath**, haga clic en la flecha desplegable y seleccione `p_orderId`. De esta forma, se configura la correlación de la segunda actividad de recepción. Para obtener más información sobre la correlación, vea [correlación](../../../../docs/framework/wcf/feature-details/correlation.md).

         ![Establecer la propiedad CorrelatesOn](./media/creating-a-long-running-workflow-service/correlateson-setting.png "establecer la propiedad CorrelatesOn.")

    5.  Arrastre y coloque una **si** actividad inmediatamente después de la **ReceiveAddItem** actividad. Esta actividad actúa como instrucción If.

        1.  Establecer el **condición** propiedad `itemId=="Zune HD" (itemId="Zune HD" for Visual Basic)`

        2.  Arrastre y coloque una **asignar** actividad en el **, a continuación,** sección y otro en el **Else** sección establece las propiedades de la **asignar** actividades, como se muestra en la siguiente ilustración.

             ![Asignar el resultado de la llamada al servicio](./media/creating-a-long-running-workflow-service/assign-result-of-service-call.png "asignar el resultado de la llamada al servicio.")

             Si la condición es `true` el **, a continuación,** sección que se va a ejecutar. Si la condición es `false` el **Else** se ejecuta la sección.

        3.  Seleccione el **SendReplyToReceive** actividad y establezca el **DisplayName** propiedad que se muestra en la siguiente ilustración.

             ![Establecer las propiedades de la actividad SendReply](./media/creating-a-long-running-workflow-service/send-reply-activity-property.png "establecer la propiedad de la actividad SendReply.")

        4.  Haga clic en el **definir...**  vincular en el **SetReplyToAddItem** actividad y configúrelo como se muestra en la siguiente ilustración. Esto configura el **SendReplyToAddItem** actividad para devolver el valor de la `orderResult` variable.

             ![Establecer el enlace de datos para la actividad SendReply](./media/creating-a-long-running-workflow-service/set-property-for-sendreplytoadditem.gif "establecer la propiedad de actividad SendReplyToAddItem.")

8. Abra el archivo web.config y agregue los siguientes elementos en la \<comportamiento > sección para habilitar la persistencia de flujo de trabajo.

    ```xml
    <sqlWorkflowInstanceStore connectionString="Data Source=your-machine\SQLExpress;Initial Catalog=SQLPersistenceStore;Integrated Security=True;Asynchronous Processing=True" instanceEncodingOption="None" instanceCompletionAction="DeleteAll" instanceLockedExceptionAction="BasicRetry" hostLockRenewalPeriod="00:00:30" runnableInstancesDetectionPeriod="00:00:02" />
              <workflowIdle timeToUnload="0"/>
    ```

    > [!WARNING]
    >  Asegúrese de reemplazar el nombre del host y de la instancia de SQL Server en el fragmento de código anterior.

9. Compile la solución.

### <a name="to-create-a-client-application-to-call-the-workflow-service"></a>Para crear una aplicación cliente que llame al servicio de flujo de trabajo

1. Agregue un nuevo proyecto de aplicación de consola denominado `OrderClient` a la solución.

2. Agregue referencias a los siguientes ensamblados al proyecto `OrderClient`

    1.  System.ServiceModel.dll

    2.  System.ServiceModel.Activities.dll

3. Agregue una referencia de servicio al servicio de flujo de trabajo y especifique `OrderService` como el espacio de nombres.

4. En el método `Main()` del proyecto de cliente, agregue el siguiente código:

    ```
    static void Main(string[] args)
    {
       // Send initial message to start the workflow service
       Console.WriteLine("Sending start message");
       StartOrderClient startProxy = new StartOrderClient();
       string orderId = startProxy.StartOrder("Kim Abercrombie");

       // The workflow service is now waiting for the second message to be sent
       Console.WriteLine("Workflow service is idle...");
       Console.WriteLine("Press [ENTER] to send an add item message to reactivate the workflow service...");
       Console.ReadLine();

       // Send the second message
       Console.WriteLine("Sending add item message");
       AddItemClient addProxy = new AddItemClient();
       AddItem item = new AddItem();
       item.p_itemId = "Zune HD";
       item.p_orderId = orderId;

       string orderResult = addProxy.AddItem(item);
       Console.WriteLine("Service returned: " + orderResult);
    }
    ```

5. Compile la solución y ejecute la aplicación `OrderClient`. El cliente mostrará un texto similar al siguiente:

    ```Output
    Sending start messageWorkflow service is idle...Press [ENTER] to send an add item message to reactivate the workflow service...
    ```

6. Para comprobar que el servicio de flujo de trabajo se ha guardado, inicie SQL Server Management Studio, vaya a la **iniciar** menú, cuando se selecciona **todos los programas**, **deMicrosoftSQLServer2008**, **SQL Server Management Studio**.

    1.  En el panel izquierdo, expanda, **bases de datos**, **SQLPersistenceStore**, **vistas** y haga clic en **System.Activities.DurableInstancing.Instances**  y seleccione **seleccionar 1000 filas superiores**. En el **resultados** panel Compruebe que aparece al menos una instancia que aparece. Puede que haya otras instancia de ejecuciones previas si se produjo una excepción durante la ejecución. Puede eliminar las filas existentes haciendo clic **System.Activities.DurableInstancing.Instances** y seleccionando **editar las primeras 200 filas**, presiona el **Execute** botón, Seleccione todas las filas en el panel de resultados y seleccione **eliminar**.  Para comprobar que la instancia que se muestra en la base de datos es la instancia de la aplicación creada, compruebe que la vista de instancias esté vacía antes de ejecutar el cliente. Una vez que se ejecute el cliente, vuelva a ejecutar la consulta (Seleccionar las primeras 1000 filas) y compruebe que se haya agregado una nueva instancia.

7. Presione Entrar para enviar y agregar un mensaje de elemento al servicio de flujo de trabajo. El cliente mostrará un texto similar al siguiente:

    ```Output
    Sending add item messageService returned: Item added to orderPress any key to continue . . .
    ```

## <a name="see-also"></a>Vea también

- [Servicios de flujo de trabajo](../../../../docs/framework/wcf/feature-details/workflow-services.md)
