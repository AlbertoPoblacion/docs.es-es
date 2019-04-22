---
title: LINQ y cadenas (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 75ddb201-d97a-4f98-8cdf-4ad51714529a
ms.openlocfilehash: 7e0ebe64494182191dafa033ecbc38bad17180be
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58818961"
---
# <a name="linq-and-strings-visual-basic"></a>LINQ y cadenas (Visual Basic)
Se puede usar LINQ para consultar y transformar cadenas y colecciones de cadenas. Puede resultar especialmente útil con datos semiestructurados de archivos de texto. Las consultas LINQ se pueden combinar con funciones de cadena tradicionales y expresiones regulares. Por ejemplo, puede usar el método <xref:System.String.Split%2A> o <xref:System.Text.RegularExpressions.Regex.Split%2A> para crear una matriz de cadenas que después puede consultar o modificar mediante LINQ. Puede usar el método <xref:System.Text.RegularExpressions.Regex.IsMatch%2A> en la cláusula `where` de una consulta LINQ. Y puede usar LINQ para consultar o modificar los resultados <xref:System.Text.RegularExpressions.MatchCollection> que se han devuelto mediante una expresión regular.  
  
 También puede usar las técnicas descritas en esta sección para transformar datos de texto semiestructurados en XML. Para obtener más información, vea [Cómo: Generar XML a partir de archivos CSV](how-to-generate-xml-from-csv-files.md).  
  
 Los ejemplos de esta sección se dividen en dos categorías:  
  
## <a name="querying-a-block-of-text"></a>Consulta de un bloque de texto  
 Puede consultar, analizar y modificar bloques de texto dividiéndolos en una matriz consultable de cadenas más pequeñas mediante el método <xref:System.String.Split%2A> o el método <xref:System.Text.RegularExpressions.Regex.Split%2A>. Puede dividir el texto de origen en palabras, frases, párrafos, páginas o cualquier otro criterio y luego realizar divisiones adicionales si son necesarias en la consulta.  
  
 [Cómo: Recuento de repeticiones de una palabra en una cadena (LINQ) (Visual Basic)](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
 Muestra cómo usar LINQ para consultas simples en texto.  
  
 [Cómo: Buscar frases que contengan un conjunto especificado de palabras (LINQ) (Visual Basic)](how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)

 Muestra cómo dividir archivos de texto en límites arbitrarios y cómo realizar consultas en cada parte.  
  
 [Cómo: Buscar caracteres en una cadena (LINQ) (Visual Basic)](how-to-query-for-characters-in-a-string-linq.md)  
 Muestra que una cadena es un tipo que se puede consultar.  
  
 [Cómo: Combinar consultas LINQ con expresiones regulares (Visual Basic)](how-to-combine-linq-queries-with-regular-expressions.md)  
 Muestra cómo usar expresiones regulares en consultas LINQ para la coincidencia de patrones compleja en resultados de consulta filtrados.  
  
## <a name="querying-semi-structured-data-in-text-format"></a>Consulta de datos semiestructurados en formato de texto  
 Muchos tipos diferentes de archivos de texto se componen de una serie de líneas, a menudo con un formato similar, como archivos delimitados por comas o líneas de longitud fija. Después de leer uno de estos archivos de texto en la memoria, puede usar LINQ para consultar o modificar las líneas. Las consultas LINQ también simplifican la tarea de combinar datos de varios orígenes.  
  
 [Cómo: Buscar la diferencia de conjuntos entre dos listas (LINQ) (Visual Basic)](how-to-find-the-set-difference-between-two-lists-linq.md)  
 Muestra cómo encontrar todas las cadenas que se encuentran en una lista pero no en la otra.  
  
 [Cómo: Ordenar o filtrar los datos de texto por palabra o campo (LINQ) (Visual Basic)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)  
 Muestra cómo ordenar líneas de texto según cualquier palabra o campo.  
  
 [Cómo: Reordenar los campos de un archivo delimitado (LINQ) (Visual Basic)](how-to-reorder-the-fields-of-a-delimited-file.md)  
 Muestra cómo cambiar el orden de los campos en una línea en un archivo .csv.  
  
 [Cómo: Combinar y comparar colecciones de cadenas (LINQ) (Visual Basic)](how-to-combine-and-compare-string-collections-linq.md)  
 Muestra cómo combinar listas de cadenas de varias maneras.  
  
 [Cómo: Rellenar colecciones de objetos de varios orígenes (LINQ) (Visual Basic)](how-to-populate-object-collections-from-multiple-sources-linq.md)  
 Muestra cómo crear colecciones de objetos mediante varios archivos de texto como orígenes de datos.  
  
 [Cómo: Combinar contenido de archivos no similares (LINQ) (Visual Basic)](how-to-join-content-from-dissimilar-files-linq.md)  
 Muestra cómo combinar cadenas de dos listas en una sola mediante una clave coincidente.  
  
 [Cómo: Dividir un archivo en varios mediante el uso de grupos (LINQ) (Visual Basic)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)  
 Muestra cómo crear nuevos archivos mediante un solo archivo como origen de datos.  
  
 [Cómo: Calcular valores de columna en un archivo de texto CSV (LINQ) (Visual Basic)](how-to-compute-column-values-in-a-csv-text-file-linq.md)  
 Muestra cómo realizar cálculos matemáticos en datos de texto en archivos .csv.  
  
## <a name="see-also"></a>Vea también

- [Language-Integrated Query (LINQ) (Visual Basic)](index.md)
- [Cómo: Generar XML a partir de archivos CSV](how-to-generate-xml-from-csv-files.md)
