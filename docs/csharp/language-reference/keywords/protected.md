---
title: Palabra clave protected (Referencia de C#)
ms.date: 07/20/2015
f1_keywords:
- protected
- protected_CSharpKeyword
helpviewer_keywords:
- protected keyword [C#]
ms.assetid: 05ce3794-6675-4025-bddb-eaaa0ec22892
ms.openlocfilehash: f25e692430f876ec384971079d6d0aa2c97e967b
ms.sourcegitcommit: fb78d8abbdb87144a3872cf154930157090dd933
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2018
ms.locfileid: "47205028"
---
# <a name="protected-c-reference"></a>protected (Referencia de C#)

La palabra clave `protected` es un modificador de acceso de miembro.

 > Esta página trata sobre el modificador de acceso `protected`. La palabra clave `protected` también forma parte de los modificadores de acceso [`protected internal`](protected-internal.md) y [`private protected`](private-protected.md).

Un miembro protegido es accesible dentro de su clase y por parte de instancias de clase derivadas.

Para obtener una comparación de `protected` con los demás modificadores de acceso, vea [Niveles de accesibilidad](accessibility-levels.md).

## <a name="example"></a>Ejemplo

Un miembro protegido de una clase base es accesible en una clase derivada únicamente si el acceso se produce a través del tipo de clase derivada. Por ejemplo, vea el siguiente segmento de código:

[!code-csharp[csrefKeywordsModifiers#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#11)]

La instrucción `a.x = 10` genera un error porque se ha creado en el método estático Main y no en una instancia de clase B.

Los miembros de estructura no se pueden proteger porque la estructura no puede heredarse.

## <a name="example"></a>Ejemplo

En este ejemplo, la clase `DerivedPoint` se deriva de `Point`. Por lo tanto, puede acceder a los miembros protegidos de la clase base directamente desde la clase derivada.

[!code-csharp[csrefKeywordsModifiers#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#12)]  

Si cambia los niveles de acceso de `x` y `y` a [private](private.md), el compilador genera los mensajes de error:

`'Point.y' is inaccessible due to its protection level.`

`'Point.x' is inaccessible due to its protection level.`

## <a name="c-language-specification"></a>especificación del lenguaje C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Vea también

- [Referencia de C#](../../../csharp/language-reference/index.md)
- [Guía de programación de C#](../../../csharp/programming-guide/index.md)
- [Palabras clave de C#](index.md)
- [Modificadores de acceso](access-modifiers.md)
- [Niveles de accesibilidad](accessibility-levels.md)
- [Modificadores](modifiers.md)
- [public](public.md)
- [private](private.md)
- [internal](internal.md)
- [Security concerns for internal virtual keywords](https://docs.microsoft.com/en-us/previous-versions/dotnet/netframework-4.0/heyd8kky(v=vs.100)) (Problemas de seguridad de palabras clave virtuales internas)