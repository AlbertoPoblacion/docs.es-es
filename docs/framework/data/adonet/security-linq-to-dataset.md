---
title: Seguridad (LINQ to DataSet)
ms.date: 03/30/2017
ms.assetid: 6116b2b8-75f4-4d8b-aea6-c13e55cda50b
ms.openlocfilehash: aa281cb4d6019ca2df85137eb505724e55b8060a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "59087344"
---
# <a name="security-linq-to-dataset"></a>Seguridad (LINQ to DataSet)
En este tema se tratan temas de seguridad en [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  
  
## <a name="passing-a-query-to-an-untrusted-component"></a>Pasar una consulta a un componente que no sea de confianza  
 Un [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] consulta se puede formular en un punto de un programa y ejecutarse en otro diferente. En el momento en que se formula la consulta, ésta puede hacer referencia a cualquier elemento visible en ese momento, como miembros privados de la clase a la que pertenece el método de llamada o símbolos que representan variables o argumentos locales. En tiempo de ejecución, la consulta podrá obtener acceso a los miembros a los que la consulta hizo referencia durante la formulación, incluso si el código de llamada no puede verlos. Al código que ejecuta la consulta no se le ha agregado visibilidad de manera arbitraria por lo que no puede elegir a qué miembro debe obtener acceso. Sólo podrá obtener acceso a lo que la consulta obtenga acceso y sólo a través de la misma consulta.  
  
 Esto implica que, al pasar una referencia a una consulta realizada a otra parte del código, el componente que recibe la consulta tiene acceso a todos los miembros públicos y privados a los que hace referencia la consulta. En general, [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] consultas no se deben pasar a componentes que no se confía, a menos que la consulta se haya construido cuidadosamente para que no expone la información que debe ser privada.  
  
## <a name="external-input"></a>Entrada externa  
 A menudo, las aplicaciones obtienen entradas externas (de un usuario o de otro agente externo) y realizan acciones basadas en dicha entrada.  En el caso de [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], la aplicación podría crear una consulta de una manera determinada, según la entrada externa o utilice dicha entrada en la consulta. Las consultas de [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] aceptan parámetros siempre que se aceptan literales. Los desarrolladores de aplicaciones deben utilizar consultas parametrizadas en lugar de insertar literales en la consulta procedentes de un agente externo.  
  
 Cualquier entrada derivada directa o indirectamente del usuario o de un agente externo puede inyectar contenido que aproveche la sintaxis del lenguaje de destino para realizar acciones no autorizadas. Esto se conoce como ataque de inyección de SQL porque en el patrón de ataque el idioma de destino es Transact-SQL. La entrada de usuario inyectada directamente en la consulta se utiliza para quitar una tabla de base de datos, provocar un ataque de denegación de servicio o cambiar la naturaleza de la operación que se está realizando. Aunque en [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] se admite la composición de consultas, se lleva a cabo a través de la API del modelo de objetos. [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] las consultas no se crean mediante el uso de manipulación de cadenas o la concatenación, ya que son en Transact-SQL y no son susceptibles de sufrir ataques de inyección SQL en el sentido tradicional.  
  
## <a name="see-also"></a>Vea también

- [Guía de programación](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)
