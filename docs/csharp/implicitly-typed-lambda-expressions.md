---
title: Expresiones lambda con tipo implícito
description: Obtenga información sobre por qué no puede usar una declaración de variable con tipo implícito para declarar una expresión lambda.
ms.date: 06/20/2016
ms.technology: csharp-advanced-concepts
ms.assetid: a3851da9-e018-4389-9922-233db7d0f841
ms.openlocfilehash: c6b0f2666a5c67ce8c89222da5959304ecb8fb93
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2019
ms.locfileid: "73039134"
---
# <a name="implicitly-typed-lambda-expressions"></a>Expresiones lambda con tipo implícito

No puede usar una declaración de variable con tipo implícito para declarar una expresión lambda.
Crea un problema de lógica circular para el compilador. La declaración `var` indica al compilador que detecte el tipo de variable del tipo de expresión en el lado derecho del operador de asignación. Una expresión lambda no tiene un tipo de tiempo de compilación, pero puede convertirse en cualquier tipo de expresión o delegado coincidente. Cuando asigna una expresión lambda a una variable de un tipo de expresión o delegado, indica al compilador que pruebe y convierta la expresión lambda en una expresión o delegado que coincida con la firma de la variable "assigned to". El compilador debe intentar que lo que se encuentra en el lado derecho de la asignación coincida con el tipo del lado izquierdo de la asignación. 

Ambos lados de la asignación no pueden indicar al compilador que se dirija al objeto del otro lado del operador de asignación y vea si coincide con el tipo.

Puede obtener más información sobre por qué el lenguaje de C# especifica ese comportamiento con la lectura de [este artículo](https://download.microsoft.com/download/5/4/B/54B83DFE-D7AA-4155-9687-B0CF58FF65D7/type-inference.pdf) (descarga de PDF).
