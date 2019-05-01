---
title: Utilizar la UI Automation para pruebas automatizadas
ms.date: 03/30/2017
helpviewer_keywords:
- automated testing
- testing, UI Automation
- UI Automation, automated testing
ms.assetid: 3a0435c0-a791-4ad7-ba92-a4c1d1231fde
ms.openlocfilehash: ad5a14ed3baab5b25cb1ed15271474580faaf176
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62033155"
---
# <a name="using-ui-automation-for-automated-testing"></a>Utilizar la UI Automation para pruebas automatizadas
> [!NOTE]
>  Esta documentación está dirigida a los desarrolladores de .NET Framework que quieran usar las clases [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] administradas definidas en el espacio de nombres <xref:System.Windows.Automation>. Para obtener información más reciente sobre [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], consulte [Windows Automation API: Automatización de interfaz de usuario](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 En esta introducción se describe cómo [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] puede ser de utilidad como marco de trabajo para el acceso mediante programación en escenarios de pruebas automatizadas.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ofrece un modelo de objetos unificado que permite a todos los marcos de trabajo [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] exponer funcionalidades complejas y enriquecidas de una manera accesible y fácil de automatizar.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] se desarrolló como sucesor de [!INCLUDE[TLA#tla_aa](../../../includes/tlasharptla-aa-md.md)]. [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] es un marco de trabajo existente diseñado para ofrecer una solución para hacer que los controles y las aplicaciones sean accesibles. [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] no se diseñó teniendo en cuenta la automatización de pruebas incluso cuando evolucionó hacia ese rol debido a los requisitos de accesibilidad y automatización muy similares. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], además de proporcionar soluciones más refinadas para mejorar la accesibilidad, de ha diseñado de manera específica para ofrecer una sólida funcionalidad para pruebas automatizadas. Por ejemplo, [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] se basa en una única interfaz tanto para exponer información sobre la interfaz de usuario como para recopilar la información necesaria para los productos de AT; [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] separa los dos modelos.  
  
 Se requieren tanto un proveedor como un cliente para implementar [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] para que sea útil como herramienta de pruebas automatizadas. Los proveedores de automatización de la interfaz de usuario son aplicaciones como Microsoft Word, Excel y otras aplicaciones de terceros o controles basados en el sistema operativo [!INCLUDE[TLA#tla_win](../../../includes/tlasharptla-win-md.md)] . Los clientes de automatización de interfaz de usuario incluyen scripts de pruebas y aplicaciones de tecnología de asistencia.  
  
> [!NOTE]
>  El propósito de esta información general es mostrar las capacidades de pruebas automatizadas nuevas y mejoradas de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Esta información general no está pensada para ofrecer información sobre las características de accesibilidad y no abordará la accesibilidad más allá de cuando sea necesario.  
  
<a name="Using_UI_Automation_During_Development"></a>   
## <a name="ui-automation-in-a-provider"></a>Automatización de la interfaz de usuario en un proveedor  
 Para que se automatice una [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] , un desarrollador de una aplicación o control debe mirar las acciones que usuario final puede llevar a cabo en el objeto [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] mediante la interacción del teclado y del mouse estándar.  
  
 Cuando se hayan identificado estas acciones de claves, los patrones de control [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] correspondientes (es decir, los patrones de control que reflejan la funcionalidad y el comportamiento del elemento [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] ) deben implementarse en el control. Por ejemplo, la interacción del usuario con un control de cuadro combinado (por ejemplo, el cuadro de diálogo Ejecutar) suele implicar expandir y contraer el cuadro combinado para ocultar o mostrar una lista de elementos, seleccionar un elemento de esa lista o agregar un nuevo valor mediante la entrada del teclado.  
  
> [!NOTE]
>  Con otros modelos de accesibilidad, los desarrolladores deben recopilar información directamente desde distintos botones, menús u otros controles individuales. Lamentablemente, cada tipo de control se presenta con docenas de pequeñas variaciones. Es decir, aunque diez variaciones de un pulsador pueden funcionar de la misma manera y realizar la misma función, todas deben tratarse como controles únicos. No hay ninguna manera de saber que estos controles sean funcionalmente equivalentes. Los patrones de control se desarrollaron para representar estos comportamientos de control comunes. Para obtener más información, consulta [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
<a name="Implementing_UI_Automation"></a>   
### <a name="implementing-ui-automation"></a>Implementación de automatización de interfaz de usuario  
 Como se ha mencionado anteriormente, sin el modelo unificado ofrecido por [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], las herramientas de prueba y los desarrolladores deben conocer la información específica del marco de trabajo para exponer propiedades y comportamientos de los controles en ese marco de trabajo. Dado que puede haber varios marcos diferentes UI presentes en cualquier momento único dentro de los sistemas operativos de Windows, incluidos [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)], [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)], y Windows Presentation Foundation (WPF), puede ser una tarea desalentadora probar varias aplicaciones con controles que parezcan similares. Por ejemplo, en la siguiente tabla se describen los nombres de propiedades específicas del marco de trabajo necesarias para recuperar el nombre (o el texto) asociado a un control de botón y se muestra la única propiedad [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] equivalente.  
  
|Tipo de control de automatización de interfaz de usuario|Marco de interfaz de usuario|Propiedad específica de marco de trabajo|Propiedad de automatización de interfaz de usuario|  
|--------------------------------|------------------|---------------------------------|----------------------------|  
|Botón|Windows Presentation Foundation|Contenido|NameProperty|  
|Botón|Win32|Título|NameProperty|  
|Imagen|HTML|alt|NameProperty|  
  
 Los proveedores de automatización de la interfaz de usuario son responsables de asignar las propiedades específicas del marco de trabajo de sus controles a las propiedades [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] equivalentes.  
  
 Encontrará a su disposición la información sobre la implementación de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] en un proveedor en [UI Automation Providers for Managed Code](../../../docs/framework/ui-automation/ui-automation-providers-for-managed-code.md). La información sobre la implementación de patrones de control está disponible en [UI Automation Control Patterns](../../../docs/framework/ui-automation/ui-automation-control-patterns.md) y [UI Automation Text Pattern](../../../docs/framework/ui-automation/ui-automation-text-pattern.md).  
  
<a name="Testing_with_UI_Automation"></a>   
## <a name="ui-automation-in-a-client"></a>Automatización de la interfaz de usuario en un cliente  
 El objetivo de muchos escenarios y herramientas de pruebas automatizadas es la manipulación coherente y repetible de la interfaz de usuario. Esto puede incluir controles específicos para pruebas de unidad a través de la grabación y reproducción de scripts de pruebas que recorrer una serie de acciones genéricas en un grupo de controles.  
  
 Una complicación que surge de las aplicaciones automatizadas es la dificultad de sincronizar una prueba con un destino dinámico. Por ejemplo, un control de cuadro de lista, como el incluido en el Administrador de tareas de Windows, que muestra una lista de aplicaciones actualmente en ejecución. Dado que los elementos del cuadro de lista se actualizan de manera dinámica fuera del control de la aplicación de prueba, resulta imposible repetir la selección de un elemento específico en el cuadro de lista con coherencia. También pueden surgir problemas similares al intentar repetir cambios de enfoque simples en una [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] que se encuentra fuera del control de la aplicación de prueba.  
  
<a name="Programmatic_Access"></a>   
### <a name="programmatic-access"></a>Acceso mediante programación  
 El acceso mediante programación ofrece la capacidad de imitar, mediante código, cualquier interacción y experiencia expuestos por mouse tradicional y entrada de teclado. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] permite el acceso mediante programación a través de cinco componentes:  
  
- El árbol [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] facilita la navegación por la estructura de la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. El árbol se crea a partir de la colección de hWnd. Para obtener más información, vea [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)  
  
- Los elementos de automatización son componentes individuales en la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. A menudo pueden ser más granulares que un hWnd. Para obtener más información, consulta [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md).  
  
- Las propiedades de automatización proporcionan información específica sobre elemento [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] . Para obtener más información, consulta [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-properties-overview.md).  
  
- Los patrones de control definen un aspecto concreto de la funcionalidad de un control; puede constar de propiedad, método, evento e información de estructura. Para obtener más información, consulta [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
- Los eventos de automatización ofrecen información y notificaciones de eventos. Para obtener más información, consulta [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
<a name="Key_properties_critical_to_test_automation"></a>   
### <a name="key-properties-for-test-automation"></a>Propiedades de clave para la automatización de pruebas  
 La capacidad de identificar de forma exclusiva y de encontrar posteriormente cualquier control dentro de la [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] ofrece la base para que las aplicaciones de pruebas automatizadas operen en esa [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]. Hay varias propiedades [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] que usan los clientes y proveedores que ayudan en esto.  
  
#### <a name="automationid"></a>AutomationID  
 Identifica de manera única un elemento de automatización de sus elementos del mismo nivel. <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> no se localiza, a diferencia de una propiedad como <xref:System.Windows.Automation.AutomationElement.NameProperty> que suele localizarse si un producto se distribuye en varios idiomas. Vea [Use the AutomationID Property](../../../docs/framework/ui-automation/use-the-automationid-property.md).  
  
> [!NOTE]
>  <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> no garantiza una identidad única en todo el árbol de automatización. Por ejemplo, una aplicación puede contener un control de menú con varios elementos de menú de nivel superior que, a su vez, tienen varios elementos de menú secundarios. Estos elementos de menú secundarios pueden identificarse mediante un esquema genérico como "Elemento1, elemento 2, Item3, etc.", lo que permite identificadores duplicados para elementos secundarios en los elementos del menú de nivel superior.  
  
#### <a name="controltype"></a>ControlType  
 Identifica el tipo de control representado por un elemento de automatización. Se puede deducir información significativa del conocimiento del tipo de control. Vea [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md).  
  
#### <a name="nameproperty"></a>NameProperty  
 Es una cadena de texto que identifica o explica un control. <xref:System.Windows.Automation.AutomationElement.NameProperty> debe usarse con precaución, ya que se puede localizar. Vea [UI Automation Properties Overview](../../../docs/framework/ui-automation/ui-automation-properties-overview.md).  
  
<a name="Steps_Required_To_Automate_the_UI_in_a_Test_Application"></a>   
### <a name="implementing-ui-automation-in-a-test-application"></a>Implementación de la automatización de interfaz de usuario en una aplicación de prueba  
  
|||  
|-|-|  
|Agregue las referencias de automatización de interfaz de usuario.|Aquí se muestran las dll [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] necesarias para los clientes de automatización de la interfaz de usuario.<br /><br /> -UIAutomationClient.dll ofrece acceso a la [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] las API del lado cliente.<br />-UIAutomationClientSideProvider.dll ofrece la posibilidad de automatizar [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] controles. Vea [UI Automation Support for Standard Controls](../../../docs/framework/ui-automation/ui-automation-support-for-standard-controls.md).<br />-UIAutomationTypes.dll ofrece acceso a los tipos específicos definidos en [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|  
|Agregue el espacio de nombres <xref:System.Windows.Automation> .|Este espacio de nombres contiene todo lo que los clientes de automatización de la interfaz de usuario necesitan para usar las capacidades de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] excepto el control del texto.|  
|Agregue el espacio de nombres <xref:System.Windows.Automation.Text> .|Este espacio de nombres contiene todo lo que un cliente de automatización de interfaz de usuario necesita para usar las capacidades de control de texto [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] .|  
|Busque controles de interés|Los scripts de pruebas automatizadas localizan elementos de automatización de la interfaz de usuario que representan controles de interés dentro del árbol de automatización.<br /><br /> Hay varias maneras de obtener elementos de automatización de interfaz de usuario con código.<br /><br /> : Consultar el [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] mediante un <xref:System.Windows.Automation.Condition> instrucción. Normalmente es donde se usa <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> independiente del lenguaje. **Nota:**  Un <xref:System.Windows.Automation.AutomationElement.AutomationIdProperty> puede obtenerse mediante una herramienta como Inspect.exe que es capaz de detallar el [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] propiedades de un control. <br /><br /> -Use el <xref:System.Windows.Automation.TreeWalker> clase para recorrer todo el [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] árbol o un subconjunto de los mismos.<br />-Realizar un seguimiento de foco.<br />-Use el hWnd del control.<br />-Use la ubicación de la pantalla, como la ubicación del cursor del mouse.<br /><br /> Vea [Obtaining UI Automation Elements](../../../docs/framework/ui-automation/obtaining-ui-automation-elements.md)|  
|Obtener patrones de control|Los patrones de control exponen comportamientos comunes para controles de funciones similares.<br /><br /> Después de encontrar los controles que requieren pruebas, los scripts de pruebas automatizadas obtienen los patrones de control de interés de los elementos de automatización de la interfaz de usuario. Por ejemplo, el patrón de control <xref:System.Windows.Automation.InvokePattern> para la funcionalidad de botón normal o el patrón de control <xref:System.Windows.Automation.WindowPattern> para la funcionalidad de la ventana.<br /><br /> Vea [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).|  
|Automatizar la interfaz de usuario|Los scripts de pruebas automatizadas pueden controlar ahora cualquier [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] de interés a partir de un marco de trabajo [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] mediante la información y la funcionalidad expuestas por los patrones de control [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] .|  
  
<a name="Supporting_tools"></a>   
## <a name="related-tools-and-technologies"></a>Herramientas y tecnologías relacionadas  
 Hay una serie de tecnologías y herramientas relacionadas que admiten pruebas automatizadas con [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
- Inspect.exe es un [!INCLUDE[TLA#tla_gui](../../../includes/tlasharptla-gui-md.md)] aplicación que puede utilizarse para recopilar [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] información para el desarrollo cliente y proveedor y depuración. Inspect.exe se incluye en el [!INCLUDE[TLA#tla_winfxsdk](../../../includes/tlasharptla-winfxsdk-md.md)].  
  
- MSAABridge expone información de [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] a los clientes de [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] . El objetivo principal de crear un puente entre [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] y [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] es permitir a los clientes existentes [!INCLUDE[TLA2#tla_aa](../../../includes/tla2sharptla-aa-md.md)] la capacidad de interactuar con cualquier marco de trabajo que ha implementado [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].  
  
<a name="Security"></a>   
## <a name="security"></a>Seguridad  
 Para obtener información de seguridad, vea [UI Automation Security Overview](../../../docs/framework/ui-automation/ui-automation-security-overview.md).  
  
## <a name="see-also"></a>Vea también

- [Aspectos básicos de Automatización de la interfaz de usuario](../../../docs/framework/ui-automation/index.md)
