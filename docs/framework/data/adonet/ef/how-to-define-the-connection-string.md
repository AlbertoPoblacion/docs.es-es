---
title: Procedimiento para defina la cadena de conexión
ms.date: 03/30/2017
ms.assetid: 6027335d-4e26-420d-9151-6523289b1989
ms.openlocfilehash: 8386f93d0e80aa824b1e91a130812b9b3a2b3619
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2019
ms.locfileid: "67306387"
---
# <a name="how-to-define-the-connection-string"></a>Procedimiento para defina la cadena de conexión

En este tema se muestra cómo definir la cadena de conexión que se usa al conectarse a un modelo conceptual. En este tema se basa en el [AdventureWorks Sales](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb387147(v=vs.100)) modelo conceptual. El modelo AdventureWorks Sales se usa en todos los temas relacionados con tareas de la documentación de [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]. En este tema se da por supuesto que ya ha configurado la [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] y define el modelo AdventureWorks Sales. Para obtener más información, vea [Cómo: Archivos de asignación y definir el modelo manualmente](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399785(v=vs.100)). Los procedimientos descritos en este tema también se incluyen en [Cómo: Configurar manualmente un proyecto de Entity Framework](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100)).

> [!NOTE]
> Si usa el Asistente para Entity Data Model en un proyecto de Visual Studio, genera automáticamente un archivo .edmx y configura el proyecto para usar el [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]. Para obtener más información, vea [Cómo: Utilice al Asistente para Entity Data Model](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))

## <a name="to-define-the-entity-framework-connection-string"></a>Para definir la cadena de conexión de Entity Framework

- Abra el archivo de configuración de la aplicación del proyecto (app.config) y, a continuación, agregue la siguiente cadena de conexión:

```xml
<connectionStrings>
    <add name="AdventureWorksEntities" 
         connectionString="metadata=.\AdventureWorks.csdl|.\AdventureWorks.ssdl|.\AdventureWorks.msl;
         provider=System.Data.SqlClient;provider connection string='Data Source=localhost;
         Initial Catalog=AdventureWorks;Integrated Security=True;Connection Timeout=60;
         multipleactiveresultsets=true'" providerName="System.Data.EntityClient" />
</connectionStrings>
```

Si el proyecto no tiene un archivo de configuración de aplicación, puede agregar uno seleccionando **Agregar nuevo elemento** desde el **proyecto** menú, seleccione el **General** categoría, seleccionar **archivo de configuración de aplicación**y, a continuación, haga clic en **agregar**.

## <a name="see-also"></a>Vea también

- [Inicio rápido](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399182(v=vs.100))
- [Cómo: Crear un nuevo archivo .edmx](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716703(v=vs.100))
- [Herramientas de Entity Data Model de ADO.NET](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
