---
title: Usar comandos para modificar datos
ms.date: 03/30/2017
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
ms.openlocfilehash: f2e3d162bfbdcb79cfecefa4ddc8e6a0dc46ee3c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "61875958"
---
# <a name="using-commands-to-modify-data"></a>Usar comandos para modificar datos
Mediante un proveedor de datos .NET Framework puede ejecutar procedimientos almacenados o instrucciones de lenguaje de definición de datos, como CREATE TABLE y ALTER COLUMN, para manipular los esquemas de una base de datos o catálogo. Estos comandos no devuelven filas como haría con una consulta, por lo que la **comando** objeto proporciona un **ExecuteNonQuery** para procesarlos.  
  
 Además de usar **ExecuteNonQuery** para modificar el esquema, también puede usar este método para procesar instrucciones SQL que modifican datos sin que no devuelven filas, como INSERT, UPDATE y DELETE.  
  
 Aunque no se devuelven filas por la **ExecuteNonQuery** pueden pasar y devolver a través de los parámetros de método de entrada y salida y valores devueltos del **parámetros** colección de la **comando**  objeto.  
  
## <a name="in-this-section"></a>En esta sección  
 [Actualización de datos de un origen de datos](../../../../docs/framework/data/adonet/updating-data-in-a-data-source.md)  
 Describe la forma de ejecutar comandos o procedimientos almacenados que modifican datos en una base de datos.  
  
 [Realización de operaciones de catálogo](../../../../docs/framework/data/adonet/performing-catalog-operations.md)  
 Describe la forma de ejecutar comandos que modifican esquemas de la base de datos.  
  
## <a name="see-also"></a>Vea también

- [Recuperar y modificar datos en ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)
- [Comandos y parámetros](../../../../docs/framework/data/adonet/commands-and-parameters.md)
- [Proveedores administrados de ADO.NET y Centro para desarrolladores de DataSet](https://go.microsoft.com/fwlink/?LinkId=217917)
