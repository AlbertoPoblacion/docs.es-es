---
title: No se pueden leer los campos delimitados porque una comilla doble no es un delimitador válido cuando EscapeQuotes se establece en True.
ms.date: 07/20/2015
f1_keywords:
- vbrTextFieldParser_IllegalDelimiter
ms.assetid: ab8a0c3a-b89c-4617-9e31-7e81f5dca433
ms.openlocfilehash: ca764d5258daf54a7149661549a78b3aca709718
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/28/2019
ms.locfileid: "64619801"
---
# <a name="unable-to-read-delimited-fields-because-a-double-quote-is-not-a-legal-delimiter-when-escapequotes-is-set-to-true"></a>No se pueden leer los campos delimitados porque una comilla doble no es un delimitador válido cuando EscapeQuotes se establece en True.
El `TextFieldParser` no se puede leer desde el archivo porque se han proporcionado comillas (") como delimitador y `EscapeQuotes` está establecido en `True`.  
  
## <a name="to-correct-this-error"></a>Para corregir este error  
  
- Establezca `EscapeQuotes` en `False`.  
  
## <a name="see-also"></a>Vea también

- [Método TextFieldParser.SetDelimiters](xref:Microsoft.VisualBasic.FileIO.TextFieldParser.SetDelimiters%2A)
- [Propiedad TextFieldParser.Delimiters](xref:Microsoft.VisualBasic.FileIO.TextFieldParser.Delimiters%2A)
- [Cómo: Leer archivos de texto delimitado por comas](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)
- [TextFieldParser (objeto)](../../visual-basic/language-reference/objects/textfieldparser-object.md)
