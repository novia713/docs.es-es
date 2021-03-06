---
title: Operador &lt;&lt; (Referencia de C#)
ms.date: 07/20/2015
f1_keywords:
- <<_CSharpKeyword
helpviewer_keywords:
- left shift operator (<<) [C#]
- << operator [C#]
ms.assetid: a654eb56-1ff7-4bf3-9064-b631be0cdccc
ms.openlocfilehash: 036acd6159bcf5ca1677ee6383c9db357625cd67
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/16/2018
ms.locfileid: "45677388"
---
# <a name="ltlt-operator-c-reference"></a>Operador &lt;&lt; (Referencia de C#)
El operador de desplazamiento a la izquierda (`<<`) desplaza su primer operando a la izquierda el número de bits especificado por su segundo operando. El tipo del segundo operando debe ser [int](../../../csharp/language-reference/keywords/int.md) o un tipo que tiene una conversión numérica implícita predefinida en `int`.  
  
## <a name="remarks"></a>Comentarios  
 Si el primer operando es [int](../../../csharp/language-reference/keywords/int.md) o [uint](../../../csharp/language-reference/keywords/uint.md) (cantidad de 32 bits), el valor de desplazamiento viene dado por los cinco bits de orden inferior del segundo operando. Es decir, el recuento de desplazamiento real es de 0 a 31 bits.  
  
 Si el primer operando es [long](../../../csharp/language-reference/keywords/long.md) o [ulong](../../../csharp/language-reference/keywords/ulong.md) (cantidad de 64 bits), el valor de desplazamiento viene dado por los seis bits de orden inferior del segundo operando. Es decir, el recuento de desplazamiento real es de 0 a 63 bits.  
  
 Se descartan los bits de orden superior que no están dentro del intervalo del tipo del primer operando después del desplazamiento y se rellenan con ceros los bits vacíos de orden inferior. Las operaciones de desplazamiento nunca producen desbordamientos.  
  
 Los tipos definidos por el usuario pueden sobrecargar el operador `<<` (vea [operator](../../../csharp/language-reference/keywords/operator.md)); el tipo del primer operando debe ser el tipo definido por el usuario y el tipo del segundo operando debe ser `int`. Cuando se sobrecarga un operador binario, el operador de asignación correspondiente, si lo hay, también se sobrecarga de modo implícito.  
  
## <a name="example"></a>Ejemplo  
 [!code-csharp[csRefOperators#14](../../../csharp/language-reference/operators/codesnippet/CSharp/left-shift-operator_1.cs)]  
  
## <a name="comments"></a>Comentarios  
 Tenga en cuenta que `i<<1` y `i<<33` dan el mismo resultado, ya que 1 y 33 tienen los mismos cinco bits de orden inferior.  
  
## <a name="see-also"></a>Vea también

- [Referencia de C#](../../../csharp/language-reference/index.md)  
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)  
- [Operadores de C#](../../../csharp/language-reference/operators/index.md)
