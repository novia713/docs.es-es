---
title: "C&#243;mo: Comprobar si las cadenas tienen un formato de correo electr&#243;nico v&#225;lido | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "expresiones regulares, ejemplos"
  - "entrada de usuario, ejemplos"
  - "Regex.IsMatch (método)"
  - "expresiones regulares [.NET Framework], ejemplos"
  - "ejemplos [Visual Basic], cadenas"
  - "IsValidEmail"
  - "validación de cadenas de correo electrónico"
  - "entrada, comprobar"
  - "cadenas [.NET Framework], ejemplos [Visual Basic]"
  - "correo electrónico [.NET Framework], validar"
  - "IsMatch (método)"
ms.assetid: 7536af08-4e86-4953-98a1-a8298623df92
caps.latest.revision: 30
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 30
---
# C&#243;mo: Comprobar si las cadenas tienen un formato de correo electr&#243;nico v&#225;lido
En el ejemplo siguiente se usa una expresión regular para comprobar que una cadena tiene un formato de correo electrónico válido.  
  
## Ejemplo  
 En el ejemplo se define un método `IsValidEmail`, que devuelve `true` si la cadena contiene una dirección de correo electrónico válida y `false` si no es válida, pero no realiza ninguna otra acción.  
  
 Para comprobar que la dirección de correo electrónico es válida, el método `IsValidEmail` llama al método <xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.MatchEvaluator%29?displayProperty=fullName> con el patrón de expresión regular `(@)(.+)$` para separar el nombre de dominio de la dirección de correo electrónico. El tercer parámetro es un delegado <xref:System.Text.RegularExpressions.MatchEvaluator> que representa el método que procesa y reemplaza el texto coincidente. El patrón de expresión regular se interpreta de esta manera:  
  
|Modelo|Descripción|  
|------------|-----------------|  
|`(@)`|Buscar el carácter @. Este es el primer grupo de captura.|  
|`(.+)`|Buscar una coincidencia con una o más apariciones de cualquier carácter. Este es el segundo grupo de captura.|  
|`$`|Finalizar la búsqueda al final de la cadena.|  
  
 El nombre de dominio junto con el carácter @ se pasa al método `DomainMapper`, que usa la clase <xref:System.Globalization.IdnMapping> para convertir los caracteres Unicode fuera del intervalo de caracteres EE.UU. \- ASCII a Punycode. El método también establece la marca `invalid` en `True` si el método <xref:System.Globalization.IdnMapping.GetAscii%2A?displayProperty=fullName> detecta cualquier carácter no válido en el nombre del dominio. El método devuelve el nombre de dominio Punycode precedido por el símbolo @ al método `IsValidEmail`.  
  
 A continuación, el método `IsValidEmail` llama al método <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=fullName> para comprobar que la dirección se ajusta a un patrón de expresión regular.  
  
 Tenga en cuenta que el método `IsValidEmail` no realiza la autenticación para validar la dirección de correo electrónico. Se limita a determinar si su formato es válido para una dirección de correo electrónico. Asimismo, el método `IsValidEmail` no comprueba que el nombre del dominio de nivel superior sea un nombre válido enumerado en la [base de datos de la zona de la raíz IANA](https://www.iana.org/domains/root/db), lo cual requeriría una operación de búsqueda. En su lugar, la expresión regular comprueba simplemente que el nombre de dominio de nivel superior conste de entre dos y veinticuatro caracteres ASCII alfanuméricos, que los caracteres primero y último sean alfanuméricos y que el resto de caracteres sean alfanuméricos o un guión \(\-\).  
  
 [!code-csharp[RegularExpressions.Examples.Email#7](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Email/cs/example4.cs#7)]
 [!code-vb[RegularExpressions.Examples.Email#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Email/vb/example4.vb#7)]  
  
 En este ejemplo, el patrón de expresión regular `^(?(")(".+?(?<!\\)"@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`\{\}\|~\w])*)(?<=[0-9a-z])@))(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z][-\w]*[0-9a-z]*\.)+[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))$` se interpreta como se muestra en la tabla siguiente. Observe que la expresión regular se compila mediante la marca <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName>.  
  
|Modelo|Descripción|  
|------------|-----------------|  
|`^`|Comenzar la búsqueda de coincidencia al principio de la cadena.|  
|`(?(")`|Determinar si el primer carácter es una comilla.`(?(")` es el principio de una construcción de alternancia.|  
|`(?("")("".+?(?<!\\)""@)`|Si el primer carácter es un signo de comillas, buscar unas comillas iniciales seguidas de al menos un carácter cualquiera, seguido a su vez de unas comillas finales. Las comillas finales no pueden ir precedidas de un carácter de barra diagonal inversa \(\\\).`(?<!` es el principio de una aserción de búsqueda anticipada negativa de ancho cero. La cadena debe concluir con una arroba \(@\).|  
|`&#124;(([0-9a-z]`|Si el primer carácter no es un signo de comillas, buscar cualquier carácter alfabético de la a a la z o de la A a la Z \(la comparación distingue entre mayúsculas y minúsculas\) o cualquier carácter numérico del 0 al 9.|  
|`(\.(?!\.))`|Si el carácter siguiente es un punto, determinar que coincide. Si no lo es, buscar más adelante en el siguiente carácter y probar si coincide.`(?!\.)` es una aserción de búsqueda anticipada negativa de ancho igual a cero que evita que aparezcan dos puntos consecutivos en la parte local de una dirección de correo electrónico.|  
|`&#124;[-!#\$%&'\*\+/=\?\^`\{\}\&#124;~\w]`|Si el carácter siguiente no es un punto, buscar cualquier carácter de palabra coincidente o uno de los siguientes caracteres: \-\!\#$%'\*\+\=?^\`{}&#124;~.|  
|`((\.(?!\.))&#124;[-!#\$%'\*\+/=\?\^`\{\}\&#124;~\w])*`|Buscar el modelo de alternancia \(un punto seguido de algo que no sea un punto, o uno de varios caracteres\) cero o más veces.|  
|`@`|Buscar el carácter @.|  
|`(?<=[0-9a-z])`|Continuar buscando si el carácter que precede al carácter @ es uno de la A a la Z, de la a a la z o del 0 al 9. La construcción `(?<=[0-9a-z])` define una aserción de búsqueda tardía positiva de ancho igual a cero.|  
|`(?(\[)`|Comprobar si el carácter que va detrás de @ es un corchete de apertura.|  
|`(\[(\d{1,3}\.){3}\d{1,3}\])`|Si lo es, buscar el corchete de apertura, seguido por una dirección IP \(cuatro grupos de uno a tres dígitos, separados por puntos\) y por un corchete de cierre.|  
|`&#124;(([0-9a-z][-\w]*[0-9a-z]*\.)+`|Si el carácter que va detrás de @ no es un corchete de apertura, buscar un carácter alfanumérico con un valor de la A a la Z, de la a a la z o del 0 al 9, seguido de cero o más apariciones de un carácter alfabético o un guion, seguido de cero o de un carácter alfanumérico con un valor de la A a la Z, de la a a la z o del 0 al 9, seguido de un punto. Este patrón se puede repetir una o más veces y debe ir seguido del nombre de dominio de nivel superior.|  
|`[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))`|El nombre de dominio de nivel superior debe empezar y finalizar por un carácter alfanumérico \(a\-z, A\-Z y 0\-9\). También puede incluir de cero a 22 caracteres ASCII que sean alfanuméricos o guiones.|  
|`$`|Finalizar la búsqueda al final de la cadena.|  
  
> [!NOTE]
>  En lugar de usar una expresión regular para validar una dirección de correo electrónico, puede usar la clase <xref:System.Net.Mail.MailAddress?displayProperty=fullName>. Para determinar si una dirección de correo es válida, pase la dirección al constructor de clases <xref:System.Net.Mail.MailAddress.%23ctor%28System.String%29?displayProperty=fullName>.  
  
## Compilar el código  
 Los métodos `IsValidEmail` y `DomainMapper` pueden estar incluidos en una biblioteca de métodos de la utilidad de expresiones regulares o pueden incluirse como métodos estáticos o de instancia privados en la clase de aplicación.  
  
 Para incluirlos en una biblioteca de expresiones regulares, tiene dos opciones: copiar y pegar el código en un proyecto de la biblioteca de clases de Visual Studio, o copiar y pegar el código en un archivo de texto y compilarlo desde la línea de comandos con un comando como el siguiente \(suponiendo que el nombre del archivo de código fuente es RegexUtilities.cs o RegexUtilities.vb:  
  
```csharp  
csc /t:library RegexUtilities.cs  
```  
  
```vb  
vbc /t:library RegexUtilities.vb  
```  
  
 También puede usar el método <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=fullName> para incluir esta expresión regular en una biblioteca de expresiones regulares.  
  
 Si se utilizan en una biblioteca de expresiones regulares, puede llamarlos utilizando código como el siguiente:  
  
 [!code-csharp[RegularExpressions.Examples.Email#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Email/cs/example4.cs#8)]
 [!code-vb[RegularExpressions.Examples.Email#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Email/vb/example4.vb#8)]  
  
 Suponiendo que haya creado una biblioteca de clases denominada RegexUtilities.dll que incluya la expresión regular de validación de correo electrónico, puede compilar este ejemplo de cualquiera de las siguientes maneras:  
  
-   En Visual Studio, cree una aplicación de consola y agregue una referencia a RegexUtilities.dll al proyecto.  
  
-   Desde la línea de comandos, copie y pegue el código fuente en un archivo de texto y compílelo con un comando como el siguiente \(suponiendo que el nombre del archivo de código fuente es Example.cs o Example.vb:  
  
    ```csharp  
    csc Example.cs /r:RegexUtilities.dll  
    ```  
  
    ```vb  
    vbc Example.vb /r:RegexUtilities.dll  
    ```  
  
## Vea también  
 [Expresiones regulares de .NET Framework](../../../docs/standard/base-types/regular-expressions.md)