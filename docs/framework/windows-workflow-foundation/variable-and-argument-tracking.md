---
title: Seguimiento de variable y argumento
ms.date: 03/30/2017
ms.assetid: 8f3d9d30-d899-49aa-b7ce-a8d0d32c4ff0
ms.openlocfilehash: ef2d6111d5c123ac6c684df09f03398340a5522c
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59231043"
---
# <a name="variable-and-argument-tracking"></a>Seguimiento de variable y argumento
Al realizar el seguimiento de la ejecución de un flujo de trabajo, a menudo resulta útil extraer los datos. Esto proporciona contexto adicional al tener acceso a un registro de seguimiento posterior a la ejecución. En [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], puede extraer cualquier variable o argumento visibles dentro del ámbito de cualquier actividad en un flujo de trabajo que use el seguimiento. Los perfiles de seguimiento facilitan la extracción de datos.  
  
## <a name="variables-and-arguments"></a>Variables y argumentos  
 Las variables y los argumentos se extraen cuando una actividad emite ActivityStateRecord.  Una variable solo está disponible para la extracción si se encuentra dentro del ámbito de la actividad. Una variable que se va a extraer de una actividad se especifica de la siguiente manera:  
  
-   Si el nombre de variable especifica una variable, el seguimiento busca la variable en la actividad actual a la que se está realizando el seguimiento y en las actividades primarias. Se busca la variable en el ámbito de actividad actual y en el ámbito primario.  
  
-   Si las variables que se va a extraer se especifican con nombre = "*", se extraerán todas las variables dentro de la actividad actual se realiza el seguimiento. En este caso, las variables que estén dentro del ámbito pero que estén definidas en actividades primarias no se extraen.  
  
 Al extraer los argumentos, los argumentos extraídos dependen del estado de la actividad. Cuando el estado de una actividad es Executing, solo están disponibles para su extracción `InArguments`. Para cualquier otro estado de actividad (Closed, Faulted, Canceled), todos los argumentos, tanto InArguments como OutArguments, estarán disponibles para la extracción.  
  
 El siguiente ejemplo muestra una consulta de estado de actividad que extrae variables y argumentos cuando se emite el registro de seguimiento de la actividad `Closed`. Los argumentos y las variables solo se pueden extraer con <xref:System.Activities.Tracking.ActivityStateRecord> y, por tanto, se suscriben en un perfil de seguimiento con <xref:System.Activities.Tracking.ActivityStateQuery>.  
  
```xml  
<activityStateQuery activityName="SendEmailActivity">  
  <states>  
    <state name="Closed"/>  
  </states>  
  <variables>  
    <variable name="FromAddress"/>  
  </variables>  
  <arguments>  
    <argument name="Result"/>  
  </arguments>  
</activityStateQuery>  
```  
  
## <a name="protecting-information-stored-within-variables-and-arguments"></a>Proteger la información almacenada dentro de variables y argumentos  
 El tiempo de ejecución de WF hace visible de manera predeterminada a la variable o argumento a los que se ha realizado el seguimiento. Un desarrollador de software del flujo de trabajo puede evitar el acceso si da los pasos siguientes:  
  
1.  Cifre el valor de una variable.  
  
2.  Controle la creación de un perfil de seguimiento para evitar la extracción de una variable o argumento.  
  
3.  En el caso de seguimiento personalizado, los participantes se aseguran de que el código WF no divulgue información confidencial que esté almacenada en variables o argumentos.  
  
## <a name="see-also"></a>Vea también

- [Supervisión de Windows Server App Fabric](https://go.microsoft.com/fwlink/?LinkId=201273)
- [Supervisión de aplicaciones con App Fabric](https://go.microsoft.com/fwlink/?LinkId=201275)
