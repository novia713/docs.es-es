---
title: /utf8output (Visual Basic) | Documentos de Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- -utf8output compiler option [Visual Basic]
- utf8output compiler option [Visual Basic]
- /utf8output compiler option [Visual Basic]
ms.assetid: 8ab36b1e-027a-49ac-85b4-f48997d9e4d6
caps.latest.revision: 11
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 89f41527703df781f32015f386bf87c1383d9769
ms.lasthandoff: 03/13/2017

---
# <a name="utf8output-visual-basic"></a>/utf8output (Visual Basic)
Muestra los resultados del compilador en codificación UTF-8.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
/utf8output[+ | -]  
```  
  
## <a name="arguments"></a>Argumentos  
 `+` &#124; `-`  
 Opcional. El valor predeterminado para esta opción es `/utf8output-`, lo que significa el resultado del compilador no utiliza la codificación UTF-8. Especificar `/utf8output` es lo mismo que especificar `/utf8output+`.  
  
## <a name="remarks"></a>Comentarios  
 En algunas configuraciones internacionales, los resultados del compilador no se muestran correctamente en la consola. En tales situaciones, utilice `/utf8output` y redirigir los resultados del compilador a un archivo.  
  
> [!NOTE]
>  El `/utf8output` opción no está disponible en el entorno de desarrollo de Visual Studio; está disponible sólo cuando se compila desde la línea de comandos.  
  
## <a name="example"></a>Ejemplo  
 El siguiente código compila `In.vb` y hace que el compilador para mostrar resultados utilizando la codificación UTF-8.  
  
```  
vbc /utf8output in.vb  
```  
  
## <a name="see-also"></a>Vea también  
 [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Líneas de comandos de compilación de ejemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)