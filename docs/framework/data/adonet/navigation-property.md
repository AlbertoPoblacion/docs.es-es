---
title: 'Propiedad de navegación: ADO.NET'
ms.date: 03/30/2017
ms.assetid: d0bf1a6a-1d84-484c-b7c3-b410fd8dc0b1
ms.openlocfilehash: afb2043abf70fa92ea7cdf8d1e8246d5cdfdba74
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73738386"
---
# <a name="navigation-property"></a>Propiedad de navegación

Una *propiedad de navegación* es una propiedad opcional en [un tipo de entidad](entity-type.md) que permite la navegación desde un [extremo](association-end.md) de una [Asociación](association-type.md) al otro extremo. A diferencia de otras [propiedades](property.md), las propiedades de navegación no contienen datos.

Una definición de propiedad de desplazamiento incluye lo siguiente:

- Un nombre. (Necesario)

- La asociación que navega. (Necesario)

- Los extremos de la asociación que navega. (Necesario)

Las propiedades de navegación son opcionales en los dos tipos de entidad de los extremos de una asociación. Si define una propiedad de navegación en un tipo de entidad del extremo de una asociación, no tiene que definir una propiedad de navegación en el tipo de entidad del otro extremo de la asociación.

El tipo de datos de una propiedad de navegación viene determinado por la [multiplicidad](association-end-multiplicity.md) de su [extremo](association-end.md)de la Asociación remota. Por ejemplo, supongamos que una propiedad de navegación, `OrdersNavProp`, existe en un tipo de entidad `Customer` y navega a una asociación uno a varios entre `Customer` y `Order`. Dado que el extremo remoto de la Asociación para la propiedad de navegación tiene la multiplicidad de muchos (\*), su tipo de datos es una colección (de `Order`). De igual forma, si una propiedad de navegación, `CustomerNavProp`, existe en el tipo de entidad `Order`, su tipo de datos sería `Customer`, porque la multiplicidad del extremo remoto es uno (1).

## <a name="example"></a>Ejemplo

El diagrama siguiente muestra un modelo conceptual con tres tipos de entidades: `Book`, `Publisher` y `Author`. Las propiedades de navegación, `Publisher` y `Authors`, se definen en el tipo de entidad Book. La propiedad de navegación `Books` se define en el tipo de entidad Publisher y el tipo de entidad `Author`.

 ![Diagrama que muestra un modelo conceptual con tres tipos de entidad.](./media/navigation-property/conceptual-model-entity-types-associations.gif)  

El [Entity Framework ADO.net](./ef/index.md) usa un lenguaje específico de dominio (DSL) denominado lenguaje de definición de esquemas conceptuales ([CSDL](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec)) para definir los modelos conceptuales. El siguiente CSDL define el tipo de entidad `Book` mostrado en el diagrama anterior.

[!code-xml[EDM_Example_Model#EntityExample](~/samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]

Observe que los atributos de XML permiten comunicar la información necesaria para definir una propiedad de navegación: el atributo `Name` contiene el nombre de la propiedad, `Relationship` contiene el nombre de la asociación que navega y `FromRole` y `ToRole` contienen los extremos de la asociación.

## <a name="see-also"></a>Vea también

- [Conceptos clave de Entity Data Model](entity-data-model-key-concepts.md)
- [Entity Data Model](entity-data-model.md)
- [Relaciones, propiedades de navegación y claves externas](/ef/ef6/fundamentals/relationships)
