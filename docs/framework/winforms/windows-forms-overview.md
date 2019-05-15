---
title: Información general sobre formularios Windows Forms
ms.date: 03/30/2017
helpviewer_keywords:
- smart clients
- Windows Forms, about Windows Forms
ms.assetid: 3a2b6284-c8d6-4e1c-8c69-0bed38f38cd4
ms.openlocfilehash: e9d117b272cea8ebb96dc579fa1d8faf65d42c45
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65583465"
---
# <a name="windows-forms-overview"></a>Información general sobre Windows Forms

La información general siguiente explica las ventajas de las aplicaciones smart client, las características principales de la programación de Windows Forms y cómo puede usar Windows Forms para compilar smart clients que satisfagan las necesidades actuales de las empresas y usuarios.

## <a name="windows-forms-and-smart-client-apps"></a>Windows Forms y aplicaciones cliente inteligentes

 Con Windows Forms, puede desarrollar aplicaciones smart client. Las aplicaciones de *cliente inteligente* son aplicaciones gráficamente enriquecidas, fáciles de implementar y actualizar, que pueden funcionar con o sin conexión a Internet y que pueden acceder a los recursos del equipo local de un modo más seguro que las aplicaciones tradicionales basadas en Windows.

### <a name="build-rich-interactive-user-interfaces"></a>Crear interfaces de usuario completas, interactivas

 Windows Forms es una tecnología de cliente inteligente para .NET Framework, un conjunto de bibliotecas administradas que simplifican tareas de aplicación comunes, como leer y escribir en el sistema de archivos. Cuando se usa un entorno de desarrollo como Visual Studio, puede crear aplicaciones smart client de Windows Forms que muestran información, soliciten la entrada de los usuarios y se comunican con equipos remotos a través de una red.

 En Windows Forms, un *formulario* es una superficie visual en la que se muestra información al usuario. Normalmente, las aplicaciones de Windows Forms se compilan mediante la adición de controles a los formularios y el desarrollo de respuestas a las acciones del usuario, como clics del mouse o presiones de teclas. Un *control* es un elemento de interfaz de usuario (UI) discreto que muestra datos o acepta la entrada de datos.

 Cuando un usuario realiza una acción en un formulario o en uno de sus controles, la acción genera un evento. La aplicación reacciona a estos eventos mediante código y procesa los eventos cuando se producen. Para más información, consulte el artículo sobre [creación de controladores de eventos en Windows Forms](creating-event-handlers-in-windows-forms.md).

 Windows Forms contiene diversos controles que puede agregar a los formularios: controles que muestran cuadros de texto, botones, cuadros desplegables, botones de radio e incluso páginas web. Para obtener una lista de todos los controles que puede usar en un formulario, consulte el artículo sobre [controles que se utilizan en formularios Windows Forms](./controls/controls-to-use-on-windows-forms.md). Si un control existente no satisface sus necesidades, Windows Forms también permite crear controles personalizados mediante la clase <xref:System.Windows.Forms.UserControl>.

 Windows Forms tiene controles de interfaz de usuario enriquecidos que emulan las características de las aplicaciones de tecnología avanzada como Microsoft Office. Los controles <xref:System.Windows.Forms.ToolStrip> y <xref:System.Windows.Forms.MenuStrip> le permiten crear barras de herramientas y menús que contienen texto e imágenes, muestran submenús y hospedan otros controles como cuadros de texto y cuadros combinados.

 Con el arrastrar y colocar **Diseñador de Windows Forms** en Visual Studio, puede crear fácilmente aplicaciones de Windows Forms. Simplemente seleccione los controles con el cursor y agréguelos donde desee en el formulario. El diseñador proporciona herramientas como líneas de cuadrícula y líneas de ajuste para minimizar la molestia de alinear los controles. Y si usa Visual Studio o compilar en la línea de comandos, puede usar el <xref:System.Windows.Forms.FlowLayoutPanel>, <xref:System.Windows.Forms.TableLayoutPanel> y <xref:System.Windows.Forms.SplitContainer> diseños de formularios de controles para crear avanzadas en menos tiempo.

 Por último, si debe crear sus propios elementos de interfaz de usuario personalizados, el espacio de nombres <xref:System.Drawing> contiene una gran selección de clases para representar líneas, círculos y otras formas directamente en un formulario.

> [!NOTE]
> Los controles de Windows Forms no están diseñados para que se serialicen entre dominios de aplicación. Por esta razón, Microsoft no admite que un control de Windows Forms traspase un límite de <xref:System.AppDomain>, ni siquiera si el tipo base <xref:System.Windows.Controls.Control> de <xref:System.MarshalByRefObject> pareciera indicar que esto es posible. Se admiten las aplicaciones de Windows Forms que tienen varios dominios de aplicación siempre y cuando no se pasen controles de Windows Forms a través de los límites del dominio de aplicación.

#### <a name="create-forms-and-controls"></a>Creación de formularios y controles

Para obtener información detallada sobre cómo usar estas características, vea los siguientes temas de ayuda.

|Descripción|Tema de ayuda|
|-----------------|----------------|
|Usar controles en formularios|[Cómo: Agregar controles a Windows Forms](./controls/how-to-add-controls-to-windows-forms.md)|
|Usar el control <xref:System.Windows.Forms.ToolStrip>|[Cómo: Crear un control ToolStrip básico con elementos estándar mediante el diseñador](./controls/create-a-basic-wf-toolstrip-with-standard-items-using-the-designer.md)|
|Crear gráficos con <xref:System.Drawing>|[Introducción a la programación de gráficos](./advanced/getting-started-with-graphics-programming.md)|
|Crear controles personalizados|[Cómo: Heredar de la clase UserControl](./controls/how-to-inherit-from-the-usercontrol-class.md)|

### <a name="display-and-manipulate-data"></a>Mostrar y manipular datos
 Muchas aplicaciones deben mostrar datos procedentes de una base de datos, archivo XML, servicio web XML u otro origen de datos. Windows Forms proporciona un control flexible denominado control <xref:System.Windows.Forms.DataGridView> para mostrar esa información tabulada en un formato tradicional de filas y columnas, de modo que cada dato ocupe su propia celda. Al usar <xref:System.Windows.Forms.DataGridView>, puede personalizar la apariencia de celdas individuales, bloquear en su posición filas y columnas arbitrarias y mostrar controles complejos dentro de las celdas, entre otras características.

 La conexión a orígenes de datos a través de una red es una tarea sencilla con las aplicaciones smart client de Windows Forms. El <xref:System.Windows.Forms.BindingSource> componente representa una conexión a un origen de datos y expone métodos para enlazar datos a controles, desplazarse por los registros anteriores y siguiente, modificar registros y guardar los cambios de vuelta al origen original. El control <xref:System.Windows.Forms.BindingNavigator> proporciona una interfaz sencilla en el componente <xref:System.Windows.Forms.BindingSource> para que los usuarios se desplacen por los registros.

 Puede crear fácilmente controles enlazados a datos en la ventana Orígenes de datos. La ventana muestra los orígenes de datos como bases de datos, servicios web y objetos en el proyecto. Para crear controles enlazados a datos, arrastre los elementos desde esta ventana hasta los formularios de su proyecto. También puede enlazar controles existentes a datos si arrastra los objetos desde la ventana Orígenes de datos a los controles existentes.

 Otro tipo de enlace de datos que puede administrar en Windows Forms es el de *configuración*. La mayoría de las aplicaciones smart client deben conservar cierta información sobre su estado de tiempo de ejecución, como el último tamaño conocido de los formularios, y conservar los datos de preferencias del usuario, como las ubicaciones predeterminadas de los archivos guardados. La característica Configuración de la aplicación aborda estos requisitos al proporcionar una manera sencilla de almacenar ambos tipos de configuración en el equipo cliente. Después de definir esta configuración mediante el uso de Visual Studio o un editor de código, la configuración se conserva con formato XML y se lee automáticamente en la memoria en tiempo de ejecución.

#### <a name="display-and-manipulate-data"></a>Mostrar y manipular datos

Para obtener información detallada sobre cómo usar estas características, vea los siguientes temas de ayuda.

|Descripción|Tema de ayuda|
|-----------------|----------------|
|Usar el componente <xref:System.Windows.Forms.BindingSource>|[Cómo: Enlazar controles de Windows Forms con el componente BindingSource mediante el diseñador](./controls/bind-wf-controls-with-the-bindingsource.md)|
|Trabajar con orígenes de datos [!INCLUDE[vstecado](../../../includes/vstecado-md.md)]|[Cómo: Ordenar y filtrar datos ADO.NET con el Windows Forms BindingSource (componente)](./controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)|
|Usar la ventana Orígenes de datos|[Enlazar controles de Windows Forms a datos en Visual Studio](/visualstudio/data-tools/bind-windows-forms-controls-to-data-in-visual-studio)|
|Usar la configuración de la aplicación|[Cómo: Crear configuración de la aplicación](./advanced/how-to-create-application-settings.md)|

### <a name="deploy-apps-to-client-computers"></a>Implementar aplicaciones en los equipos cliente

Una vez escrita la aplicación, hay que enviarla a los usuarios para que puedan instalarla y ejecutarla en sus equipos cliente. Cuando se usa el [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] tecnología, puede implementar aplicaciones desde Visual Studio con tan solo unos clics y proporcionar a los usuarios con una dirección URL que apunte a la aplicación en la Web. [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] administra todos los elementos y dependencias de la aplicación y garantiza que está instalada correctamente en el equipo cliente.

Las aplicaciones [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] se pueden configurar para ejecutarse únicamente cuando el usuario está conectado a la red, o para ejecutarse tanto en línea como sin conexión. Al especificar que una aplicación debe admitir el funcionamiento sin conexión, [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] agrega un vínculo a la aplicación en el menú **Inicio** del usuario. El usuario puede entonces abrir la aplicación sin usar la dirección URL.

Cuando se actualiza la aplicación, se publica un nuevo manifiesto de implementación y una nueva copia de la aplicación en el servidor web. [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] detectará que hay una actualización disponible y actualizará la instalación del usuario; no se requiere ninguna programación personalizada para actualizar los ensamblados antiguos.

#### <a name="deploy-clickonce-apps"></a>Implementar aplicaciones ClickOnce

Para obtener una introducción completa a [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)], consulte [Seguridad e implementación ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment). Para obtener información detallada sobre cómo usar estas características, vea los siguientes temas de ayuda.

|Descripción|Tema de ayuda|
|-----------------|----------------|
|Implementar una aplicación mediante [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]|[Cómo: Publicación de una aplicación ClickOnce mediante el Asistente para publicación](/visualstudio/deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard)<br /><br /> [Tutorial: Implementación manual de una aplicación ClickOnce](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)|
|Actualizar una implementación [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]|[Cómo: Administración de actualizaciones de aplicaciones ClickOnce](/visualstudio/deployment/how-to-manage-updates-for-a-clickonce-application)|
|Administrar la seguridad con [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]|[Cómo: Habilitación de la configuración de seguridad ClickOnce](/visualstudio/deployment/how-to-enable-clickonce-security-settings)|

### <a name="other-controls-and-features"></a>Otros controles y características

Hay muchas otras características en Windows Forms que simplifican y agilizan las tareas comunes de implementación, como la posibilidad de crear cuadros de diálogo, imprimir, agregar ayuda y documentación, y localizar la aplicación a varios idiomas. Además, Windows Forms se basa en el sólido sistema de seguridad de .NET Framework. Con este sistema, puede publicar aplicaciones más seguras para sus clientes.

#### <a name="implement-other-controls-and-features"></a>Implementar otros controles y características

Para obtener información detallada sobre cómo usar estas características, vea los siguientes temas de ayuda.

|Descripción|Tema de ayuda|
|-----------------|----------------|
|Imprimir el contenido de un formulario|[Cómo: Imprimir gráficos en Windows Forms](./advanced/how-to-print-graphics-in-windows-forms.md)<br /><br /> [Cómo: Imprimir un archivo de texto de varias páginas en Windows Forms](./advanced/how-to-print-a-multi-page-text-file-in-windows-forms.md)|
|Más información sobre la seguridad de Windows Forms|[Información general sobre la seguridad en Windows Forms](security-in-windows-forms-overview.md)|

## <a name="see-also"></a>Vea también

- [Introducción a los formularios Windows Forms](getting-started-with-windows-forms.md)
- [Crear un nuevo formulario Windows Forms](creating-a-new-windows-form.md)
- [Información sobre el control ToolStrip](./controls/toolstrip-control-overview-windows-forms.md)
- [Información general del control DataGridView](./controls/datagridview-control-overview-windows-forms.md)
- [Información general sobre el componente BindingSource](./controls/bindingsource-component-overview.md)
- [Introducción a la configuración de la aplicación](./advanced/application-settings-overview.md)
- [Seguridad e implementación ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment)
