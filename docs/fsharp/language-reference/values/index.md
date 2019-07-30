---
title: Valores
description: Obtenga información sobre cómo F# los valores de son cantidades que tienen un tipo específico.
ms.date: 05/16/2016
ms.openlocfilehash: ed7a5b069a5a47aacf0cce4cfa754ded46f6e84a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630801"
---
# <a name="values"></a>Valores

Los valores de F# son cantidades que tienen un tipo específico. Los valores pueden ser números enteros o de punto flotante, caracteres o texto, listas, secuencias, matrices, tuplas, uniones discriminadas, registros, tipos de clase o valores de función.

## <a name="binding-a-value"></a>Enlace de un valor

El término *enlace* significa asociar un nombre a una definición. La palabra clave `let` enlaza un valor, como en los ejemplos siguientes:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet601.fs)]

El tipo de un valor se infiere de la definición. Para un tipo primitivo, como un número entero o de punto flotante, el tipo se determina a partir del tipo del literal. Por tanto, en el ejemplo anterior, el compilador infiere que el tipo de `b` es `unsigned int`, mientras que el compilador infiere que el tipo de `a` es `int`. El tipo de un valor de función se determina a partir del valor devuelto en el cuerpo de la función. Para más información sobre los tipos de valor de función, vea [Funciones](../functions/index.md). Para más información sobre los tipos literales, vea [Literals](../literals.md) (Literales).

De forma predeterminada, el compilador no emite diagnósticos sobre los enlaces no utilizados. Para recibir estos mensajes, habilite la advertencia 1182 en el archivo del proyecto o al invocar al compilador (vea `--warnon` en [Opciones del compilador](../compiler-options.md)).

## <a name="why-immutable"></a>¿Por qué inmutables?

Los valores inmutables son valores que no se pueden cambiar durante el transcurso de la ejecución de un programa. Si está habituado a usar lenguajes como C++, Visual Basic o C#, le resultará sorprendente que F# dé prioridad a los valores inmutables y no a las variables, a las que se pueden asignar nuevos valores durante la ejecución de un programa. Los datos inmutables son un elemento importante de la programación funcional. En un entorno multiproceso, resulta complicado administrar las variables mutables compartidas, dado que pueden modificarlas muchos subprocesos diferentes. Además, con las variables mutables, a veces puede resultar difícil saber si existe la posibilidad de que una variable haya cambiado cuando se pasa a otra función.

En los lenguajes funcionales puros, no hay variables y las funciones se comportan estrictamente como funciones matemáticas. Cuando el código de un lenguaje de procedimientos usa una asignación de variable para modificar un valor, el código equivalente de un lenguaje funcional tiene un valor inmutable que es la entrada, una función inmutable y distintos valores inmutables como salida. Esta rigidez matemática permite un razonamiento más estricto sobre el comportamiento del programa. Y este razonamiento más estricto es lo que permite a los compiladores comprobar el código de una manera más rigurosa y optimizar con mayor eficacia, además de hacer que a los desarrolladores de software les resulte más fácil entender y escribir código correcto. Por tanto, es probable que el código funcional sea más fácil de depurar que el código de procedimientos ordinario.

Aunque F# no es un lenguaje funcional puro, admite plenamente la programación funcional. El uso de valores inmutables es una práctica correcta porque permite que el código se beneficie de un aspecto importante de la programación funcional.

## <a name="mutable-variables"></a>Variables mutables

Se puede usar la palabra clave `mutable` para especificar una variable que se puede cambiar. En F#, en general las variables mutables deben tener un ámbito limitado, ya sea como campo de un tipo o bien como valor local. Las variables mutables con un ámbito limitado son más fáciles de controlar y es menos probable que se modifiquen de manera incorrecta.

Se puede asignar un valor inicial a una variable mutable mediante la palabra clave `let` de la misma manera que se define un valor. Pero la diferencia reside en que, posteriormente, se pueden asignar nuevos valores a las variables mutables mediante el operador `<-`, como en el ejemplo siguiente.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet602.fs)]

Los valores `mutable` marcados se pueden promover `'a ref` automáticamente a si se capturan mediante un cierre, incluidos los formularios que crean `seq` cierres, como los generadores. Si desea recibir una notificación cuando esto suceda, habilite la advertencia 3180 en el archivo del proyecto o al invocar al compilador.

## <a name="related-topics"></a>Temas relacionados

|Título|DESCRIPCIÓN|
|-----|-----------|
|[Enlaces let](../functions/let-bindings.md)|Proporciona información sobre el uso `let` de la palabra clave para enlazar nombres a valores y funciones.|
|[Funciones](../functions/index.md)|Proporciona información general sobre las funciones en F#.|

## <a name="see-also"></a>Vea también

- [Valores NULL](null-Values.md)
- [Referencia del lenguaje F#](../index.md)
