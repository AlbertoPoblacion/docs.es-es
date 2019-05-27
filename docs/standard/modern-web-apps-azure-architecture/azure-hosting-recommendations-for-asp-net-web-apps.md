---
title: Recomendaciones de hospedaje en Azure de aplicaciones web ASP.NET Core
description: Aplicaciones web modernas con ASP.NET Core y Azure | Recomendaciones de hospedaje en Azure de aplicaciones web ASP.NET Core
author: ardalis
ms.author: wiwagn
ms.date: 01/30/2019
ms.openlocfilehash: a93009e66d63aa7d9c3b60951d43eafa3c351a63
ms.sourcegitcommit: 7e129d879ddb42a8b4334eee35727afe3d437952
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66053263"
---
# <a name="azure-hosting-recommendations-for-aspnet-core-web-apps"></a>Recomendaciones de hospedaje en Azure de aplicaciones web ASP.NET Core

> "Los líderes de línea de negocio en todas partes evitan a los departamentos de TI para obtener aplicaciones de la nube (también conocidas como SaaS) y pagar por ellas como harían con la suscripción a una revista. Y cuando el servicio ya no es necesario, pueden cancelar la suscripción sin dejar ningún equipo sin usar en un rincón".  
> _\- Daryl Plummer, analista de Gartner_

Windows Azure es capaz de admitir las necesidades y la arquitectura de la aplicación. Las necesidades de hospedaje pueden ser tan simples como un sitio web estático a una aplicación sofisticada formada por decenas de servicios. Para las aplicaciones web monolíticas de ASP.NET Core y los servicios complementarios, se recomiendan varias configuraciones conocidas. Las recomendaciones de este artículo se agrupan según el tipo de recurso que se va a hospedar, ya sean aplicaciones completas, procesos individuales o datos.

## <a name="web-applications"></a>Aplicaciones web

Las aplicaciones web se pueden hospedar con:

- App Service Web Apps

- Contenedores

- Máquinas virtuales (VM)

De estas, App Service Web Apps es el enfoque recomendado para la mayoría de los escenarios. Para las arquitecturas de microservicios, considere la posibilidad de un enfoque basado en contenedores. Si necesita más control sobre los equipos que ejecutan la aplicación, considere la posibilidad de Azure Virtual Machines.

### <a name="app-service-web-apps"></a>App Service Web Apps

App Service Web Apps proporciona una plataforma totalmente administrada optimizada para el hospedaje de aplicaciones web. Es una oferta de plataforma como servicio (PaaS) que permite centrarse en la lógica de negocios, mientras Azure se encarga de la infraestructura necesaria para ejecutar y escalar la aplicación. Algunas características clave de App Service Web Apps son estas:

- Optimización de DevOps (integración y entrega continuas, varios entornos, pruebas A/B, compatibilidad con scripting).

- Escala global y alta disponibilidad.

- Conexiones a plataformas SaaS y datos locales.

- Seguridad y cumplimiento.

- Integración de Visual Studio.

- Compatibilidad con contenedores de Linux y Windows a través de [Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).

Azure App Service es la mejor opción para la mayoría de las aplicaciones web. La implementación y la administración se integran en la plataforma, los sitios se pueden escalar rápidamente para controlar grandes cargas de tráfico y el administrador de tráfico y equilibrio de carga integrado proporcionan alta disponibilidad. Puede mover fácilmente los sitios existentes a Azure App Service con una herramienta de migración en línea, usar una aplicación de código abierto de la Galería de aplicaciones web o crear un sitio con el marco y las herramientas que elija. La característica WebJobs facilita agregar el procesamiento de trabajos en segundo plano a la aplicación web de App Service.

### <a name="azure-kubernetes-service"></a>Azure Kubernetes Service

Azure Kubernetes Service (AKS) administra el entorno hospedado de Kubernetes, lo que acelera y facilita la implementación y administración de aplicaciones en contenedores sin necesidad de tener conocimientos de orquestación de contenedores. También se elimina la carga de las operaciones en curso y del mantenimiento mediante el aprovisionamiento, la actualización y el escalado de los recursos a petición, sin tener que desconectar las aplicaciones.

AKS reduce la complejidad y la sobrecarga operativa de la administración de un clúster de Kubernetes mediante la descarga de gran parte de esa responsabilidad en Azure. Como un servicio de Kubernetes hospedado, Azure controla de forma automática tareas críticas como el seguimiento de estado y el mantenimiento. Además, solo se paga por los nodos de agente en los clústeres, no por los nodos principales. Como servicio de Kubernetes administrado, AKS proporciona lo siguiente:

- Actualizaciones de la versión de Kubernetes automatizadas y aplicación de revisiones.
- Escalado de clústeres sencillo.
- Plano de control hospedado de recuperación automática (nodos principales).
- Ahorro de costos: pague solo por los nodos de grupo de agentes en ejecución.

Como Azure controla la administración de los nodos del clúster de AKS, ya no es necesario realizar muchas tareas manualmente, como las actualizaciones del clúster. Como Azure controla estas tareas de mantenimiento críticas de forma automática, AKS no proporciona acceso directo al clúster (por ejemplo con SSH).

### <a name="azure-virtual-machines"></a>Azure Virtual Machines

Si tiene una aplicación existente que requeriría modificaciones importantes para ejecutarse en App Service, podría elegir Virtual Machines con el fin de simplificar la migración a la nube. Aunque la configuración, la protección y el mantenimiento correctos de las máquinas virtuales requiere mucho más tiempo y experiencia en TI en comparación con Azure App Service. Si está pensando en Azure Virtual Machines, asegúrese de tener en cuenta el esfuerzo de mantenimiento continuado necesario para aplicar revisiones, actualizar y administrar el entorno de máquinas virtuales. Azure Virtual Machines es una infraestructura como servicio (IaaS), mientras que App Service es PaaS. También debe considerar si la implementación de la aplicación como un contenedor de Windows en Web App for Containers podría ser una opción viable para su escenario.

## <a name="logical-processes"></a>Procesos lógicos

Los procesos lógicos individuales que se pueden desacoplar del resto de la aplicación se pueden implementar por separado en Azure Functions de forma "sin servidor". Azure Functions permite escribir simplemente el código que se necesita para un problema determinado, sin preocuparse por la aplicación o infraestructura para ejecutarlo. Se puede elegir entre una variedad de lenguajes de programación, incluyendo C\#, F\#, Node.js, Python y PHP, lo que permite elegir el lenguaje más productivo para la tarea en cuestión. Al igual que la mayoría de las soluciones basadas en la nube, solo se paga por la cantidad de tiempo que se usa y se puede confiar en Azure Functions para escalar verticalmente según sea necesario.

## <a name="data"></a>Datos

Azure ofrece una amplia variedad de opciones de almacenamiento de datos, por lo que la aplicación puede usar el proveedor de datos adecuado para los datos en cuestión.

Para los datos transaccionales y relacionales, Azure SQL Database es la mejor opción. Para los datos de alto rendimiento y principalmente de solo lectura, una caché en Redis respaldada por Azure SQL Database es una buena solución.

Los datos JSON no estructurados se pueden almacenar de diferentes formas, desde columnas de SQL Database a Blobs o Tablas de Azure Storage, a DocumentDB. De todos estos, DocumentDB ofrece la mejor funcionalidad de consulta y es la opción recomendada para un gran número de documentos basados en JSON que deben admitir las consultas.

Los datos transitorios basados en eventos o comandos que se usan para coordinar el comportamiento de la aplicación pueden usar Azure Service Bus o Azure Storage Queue. Azure Storage Bus ofrece más flexibilidad y es el servicio recomendado para mensajería no trivial dentro y entre las aplicaciones.

## <a name="architecture-recommendations"></a>Recomendaciones de arquitectura

Los requisitos de la aplicación deben dictar su arquitectura. Hay muchos servicios de Azure diferentes disponibles. Elegir el adecuado es una decisión importante. Microsoft ofrece una galería de arquitecturas de referencia para ayudar a identificar arquitecturas típicas optimizadas para escenarios comunes. Es posible que encuentre una arquitectura de referencia estrechamente relacionada con los requisitos de la aplicación o, que al menos, ofrezca un punto de partida.

En la figura 11-2 se muestra una arquitectura de referencia de ejemplo. En este diagrama se describe un enfoque de arquitectura recomendada para un sitio web del sistema de administración de contenido de Sitecore optimizado para marketing.

![](./media/image11-2.png)

**Figura 11-1.** Arquitectura de referencia del sitio web de marketing Sitecore.

**Referencias: recomendaciones de hospedaje de Azure**

- Arquitecturas de soluciones de Azure\
  <https://azure.microsoft.com/solutions/architecture/>

- Guía para desarrolladores de Microsoft Azure\
  <https://azure.microsoft.com/campaigns/developer-guide/>

- Información general de Web Apps\
  <https://docs.microsoft.com/azure/app-service/app-service-web-overview>

- Web App for Containers\
  <https://azure.microsoft.com/services/app-service/containers/>

- Introducción a Azure Kubernetes Service (AKS)\
  <https://docs.microsoft.com/azure/aks/intro-kubernetes>

>[!div class="step-by-step"]
>[Anterior](development-process-for-azure.md)
