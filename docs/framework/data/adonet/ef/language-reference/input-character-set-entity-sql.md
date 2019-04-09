---
title: Juego de caracteres de entrada (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 13d291d3-e6bc-4719-b953-758b61a590b6
ms.openlocfilehash: 3795660cf6086aa67596f31e49c4d950aa653d86
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59109733"
---
# <a name="input-character-set-entity-sql"></a>Juego de caracteres de entrada (Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] acepta caracteres UNICODE codificados en UTF-16.  
  
 Los literales de cadena pueden contener cualquier carácter UTF-16 entre comillas simples. Por ejemplo, N'文字列リテラル'. Cuando se comparan literales de cadena, se usan los valores UTF-16 originales. Por ejemplo, N'ABC' es diferente en las páginas de códigos japonesa y latina.  
  
 Los comentarios pueden contener cualquier carácter UTF-16.  
  
 Los identificadores de escape pueden contener cualquier carácter UTF-16 entre corchetes. Por ejemplo, [エスケープされた識別子]. La comparación de identificadores de escape UTF-16 no distingue mayúsculas de minúsculas. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] trata las versiones de letras que parecen iguales pero proceden de páginas de códigos diferentes como caracteres distintos. Por ejemplo, [ABC] es equivalente a [abc] si los caracteres correspondientes son de la misma página de códigos. Sin embargo, si los mismos dos identificadores son de páginas de códigos distintas, no son equivalentes.  
  
 El espacio en blanco es cualquier carácter de espacio en blanco UTF-16.  
  
 Una línea nueva es cualquier carácter de nueva línea UTF-16 normalizado. Por ejemplo, '\n' y '\r\n' se consideran caracteres de nueva línea, pero '\r' no es un carácter de nueva línea.  
  
 Las palabras clave, las expresiones y los signos de puntuación pueden ser cualquier carácter UTF-16 que se normalice a caracteres latinos. Por ejemplo, SELECT en una página de códigos japonesa es una palabra clave válida.  
  
 Las palabras clave, las expresiones y los signos de puntuación solo pueden ser caracteres latinos. `SELECT` en una página de códigos japonesa no es una palabra clave. +,-, \*, /, =, (,), ', [,] y cualquier otra construcción de lenguaje no las mencionadas aquí solo puede ser caracteres latinos.  
  
 Los identificadores simples solo pueden ser caracteres latinos. Esto evita la ambigüedad durante la comparación, ya que se comparan valores originales. Por ejemplo, ABC sería diferente en las páginas de códigos japonesa y latina.  
  
## <a name="see-also"></a>Vea también

- [Información general sobre Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)
