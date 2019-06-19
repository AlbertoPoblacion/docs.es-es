---
title: Administración de entornos de Docker en producción
description: Familiarícese con los puntos clave para administrar un entorno de producción basado en contenedores.
ms.date: 02/15/2019
ms.openlocfilehash: 7d10f670745f8bac1084b8c33c5acde67bac6229
ms.sourcegitcommit: 5bc85ad81d96b8dc2a90ce53bada475ee5662c44
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/13/2019
ms.locfileid: "65641071"
---
# <a name="manage-production-docker-environments"></a>Administración de entornos de Docker en producción

El proceso de administrar y orquestar un clúster consiste en controlar un grupo de hosts. Esto puede conllevar agregar y eliminar hosts de un clúster, obtener información sobre el estado actual de los hosts y los contenedores, e iniciar y detener los procesos. La administración y la orquestación del clúster están estrechamente relacionadas con la programación, dado que el programador debe tener acceso a cada host del clúster a fin de programar servicios. Por este motivo, suele usarse la misma herramienta para ambos fines.

## <a name="container-service-and-management-tools"></a>Servicio de contenedor y herramientas de administración

El servicio de contenedor proporciona una rápida implementación de agrupación en clústeres de contenedor de código abierto y soluciones de orquestación populares. Usa imágenes de Docker para asegurarse de que los contenedores de la aplicación sean totalmente portátiles. Mediante el servicio de contenedor, puede implementar clústeres de DC/OS (con tecnología de Mesosphere y Apache Mesos) y Docker Swarm con plantillas de Azure Resource Manager o Azure Portal para asegurarse de poder escalar estas aplicaciones a miles de contenedores, o incluso a decenas de miles.

Estos clústeres se implementan mediante Conjuntos de escala de máquinas virtuales de Azure y sacan provecho de las posibilidades que ofrecen las funciones de red y almacenamiento de Azure. Para acceder al servicio de contenedor, necesita una suscripción de Azure. Con el servicio de contenedor, puede sacar provecho de las características de nivel empresarial de Azure manteniendo la portabilidad de la aplicación, incluso en las capas de orquestación.

En la tabla 6-1 se enumeran las herramientas de administración comunes relacionadas con los orquestadores, los programadores y la plataforma de agrupación en clústeres.

**Tabla 6-1**. Herramientas de administración de Docker

| Herramientas de administración | Descripción | Orquestadores relacionados |
|------------------|-------------|-----------------------|
| [Azure Monitor para contenedores](https://docs.microsoft.com/azure/monitoring/monitoring-container-insights-overview) | Herramienta de administración de Kubernetes dedicada a Azure. | Azure Kubernetes Services (AKS) |
| [Interfaz de usuario web de Kubernetes (panel)](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) | Herramienta de administración de Kubernetes que puede supervisar y administrar un clúster local de Kubernetes. | Azure Kubernetes Service (AKS)<br/>Kubernetes local |
| [Azure Portal para Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal)<br/>[Azure Service Fabric Explorer](https://docs.microsoft.com/azure/service-fabric/service-fabric-visualizing-your-cluster) | Versión de escritorio y en línea para administrar clústeres de Service Fabric en Azure, en el entorno local, en el desarrollo local y en otras nubes. | Azure Service Fabric |
| [Supervisión de contenedores (Azure Monitor)](https://docs.microsoft.com/azure/azure-monitor/insights/containers) | Administración de contenedores general y solución de supervisión. Puede administrar clústeres de Kubernetes mediante [Azure Monitor para contenedores](https://docs.microsoft.com/azure/monitoring/monitoring-container-insights-overview). | Azure Service Fabric<br/>Azure Kubernetes Service (AKS)<br/>Mesosphere DC/OS y otros |

## <a name="azure-service-fabric"></a>Azure Service Fabric

Otra opción para la administración y la implementación del clúster es Azure Service Fabric. [Service Fabric](https://azure.microsoft.com/services/service-fabric/) es una plataforma de microservicios de Microsoft que incluye la orquestación de contenedores, así como modelos de programación para desarrolladores que permiten compilar aplicaciones de microservicios altamente escalables. Service Fabric es compatible con Docker en contenedores de Windows y Linux y se puede ejecutar en servidores de Windows y Linux.

A continuación se enumeran herramientas de administración de Service Fabric:

- [Azure Portal para Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-portal) permite llevar a cabo en un clúster operaciones relacionadas con este (crear, actualizar o eliminar) o configurar su infraestructura (máquinas virtuales, equilibrador de carga, redes, etc.).

- [Azure Service Fabric Explorer](https://docs.microsoft.com/azure/service-fabric/service-fabric-visualizing-your-cluster) es una herramienta multiplataforma de escritorio e interfaz de usuario web especializada que proporciona información y permite realizar ciertas operaciones en el clúster de Service Fabric, desde el punto de vista de los nodos o las máquinas virtuales y desde el punto de vista de la aplicación y los servicios.

>[!div class="step-by-step"]
>[Anterior](run-microservices-based-applications-in-production.md)
>[Siguiente](monitor-containerized-application-services.md)
