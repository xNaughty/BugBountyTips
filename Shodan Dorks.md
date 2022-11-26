# Shodan Dorks
Shodan es un motor de búsqueda que sirve para encontrar dispositivos conectados a internet, desde routers, APs, dispositivos IoT hasta cámaras de seguridad y mucho más

## Filtros de Shodan

### City
Encuentra dispositivos en una ciudad en particular

    city:"buenos aires"
    
### Country
Encuentra dispositivos en un país en particular

    country:"AR"
    
### Geo
Encuentre dispositivos dando coordenadas geográficas

    geo:"56.913055,118.250862"
    
### Location

    country:ar
    city:buenos aires
    country:ar city:buenos aires
    
### Hostname  
Encuentre dispositivos que coincidan con el nombre de host

    server: "gws" hostname:"google"
    hostname:example.com
    hostname:example.com,example.org
    
### Net
Encuentre dispositivos basados en una dirección IP o /x CIDR

    net:210.214.0.0/16
    
### Organization

    org:microsoft
    org:"United States Department"
    
### Autonomous System Number (ASN)

    asn:ASxxxx
    
### Operating System
Encuentre dispositivos basados en el sistema operativo

    os:"windows 7"
    os:"windows server 2012"
    os:"linux 3.x"
    
### Port
Encuentre dispositivos basados en puertos abiertos

    ftp port:21
    
### Before/after
Encuentre dispositivos antes o después entre un tiempo determinado

    apache after:22/02/2009 before:14/3/2010
    
### SSL/TLS Certificates
- Certificados autofirmados 

      ssl.cert.issuer.cn:example.com ssl.cert.subject.cn:example.com
      
- Certificados caducados 

      ssl.cert.expired:true
      ssl.cert.subject.cn:example.com     
      
### Tipo de dispositivo 

    device:firewall
    device:router
    device:wap
    device:webcam
    device:media
    device:"broadband router"
    device:pbx
    device:printer
    device:switch
    device:storage
    device:specialized
    device:phone
    device:"voip phone"
    device:"voip adaptor"
    device:"load balancer"
    device:"print server"
    device:terminal
    device:remote
    device:telecom
    device:power
    device:proxy
    device:pda
    device:bridge
    
### Product

    product:apache
    product:nginx
    product:android
    product:chromecast
    
### Customer Premises Equipment (CPE)

    cpe:apple
    cpe:microsoft
    cpe:nginx
    cpe:cisco
    
### Server

    server: nginx
    server: apache
    server: microsoft
    server: cisco-ios
    
### ssh fingerprints

    dc:14:de:8e:d7:c1:15:43:23:82:25:81:d2:59:e8:c0
    
## Web

### Pulse Secure

    http.html:/dana-na
    
### PEM Certificates

    http.title:"Index of /" http.html:".pem"
    
## Base de datos

### MySQL

    "product:MySQL"
    
### MongoDB

    "product:MongoDB"
    
### elastic

    port:9200 json
    
### Memcached

    "product:Memcached"
    
### CouchDB

    "product:CouchDB"
    
### PostgreSQL

    "port:5432 PostgreSQL"
    
### Riak

    "port:8087 Riak"
    
### Redis

    "product:Redis"
    
### Cassandra

    "product:Cassandra"
    
## Sistemas de Control Industrial 

### Vallas publicitarias electrónicas de Samsung 

    "Server: Prismview Player"
    
### Controladores de bombas de gasolineras 

    "in-tank inventory" port:10001
    
### Bombas de combustible conectadas a internet
No se requiere autenticación para acceder al terminal CLI

    "privileged command" GET
    
### Lectores automáticos de matrículas     

    P372 "ANPR enabled"
    
### Controladores de Semáforos / Cámaras de Luz Roja

    mikrotik streetlight
    
### Máquinas de votación en los Estados Unidos 

    "voter system serial" country:US
    
### Abrir cajero automático

    May allow for ATM Access availability
    NCR Port:"161"
    
### Empresas de telecomunicaciones que ejecutan escuchas telefónicas de intercepción legal de Cisco

    "Cisco IOS" "ADVIPSERVICESK9_LI-M"
    
### Teléfonos públicos de prisiones 

    "[2J[H Encartele Confidential"
    
### Estado de carga del PowerPack de Tesla 

    http.title:"Tesla PowerPack System" http.component:"d3" -ga3ca4f2
    
### Cargadores de vehículos eléctricos 

    "Server: gSOAP/2.8" "Content-Length: 583"
    
### Satélites marítimos 
¡Shodan creó un rastreador de barcos bastante bueno que también mapea las ubicaciones de los barcos en tiempo real! 

    "Cobham SATCOM" OR ("Sailor" "VSAT")
    
### Tableros de Control de Misión Submarina 

    title:"Slocum Fleet Mission Control"
    
### CAREL PlantVisor Grupos Frigoríficos 

    "Server: CarelDataServer" "200 Document follows"
    
### Parques de aerogeneradores Nordex 

    http.title:"Nordex Control" "Windows 2000 5.0 x86" "Jetty/3.1 (JSP 1.1; Servlet 2.2; java 1.6.0_14)"
    
### Rastreadores GPS para vehículos comerciales C4 Max 

    "[1m[35mWelcome on console"
    
### Máquinas de rayos X médicas DICOM     
Seguro por defecto, afortunadamente, pero estas más de 1700 máquinas aún no tienen nada que hacer en Internet

    "DICOM Server Response" port:104
    
### Medidores de electricidad de GaugeTech 

    "Server: EIG Embedded Web Server" "200 Document follows"
    
### Siemens Automatización Industrial 

    "Siemens, SIMATIC" port:161
    
### Controladores HVAC de Siemens 

      "Server: Microsoft-WinCE" "Content-Length: 12581"
      
### Controladores de acceso para puertas y cerraduras 

    "HID VertX" port:4070
    
### Gestión Ferroviaria 

    "log off" "select the appropriate"
    
### Estado de carga del Powerpack de Tesla
Ayuda a encontrar el estado de carga de tesla powerpack

    http.title:"Tesla PowerPack System" http.component:"d3" -ga3ca4f2
    
### Aerogenerador XZERES 

    title:"xzeres wind"
    
### Lector de matrículas automático PIPS 

    "html:"PIPS Technology ALPR Processors""
    
### Modbus 

    "port:502"
    
### Niagara Fox

    "port:1911,4911 product:Niagara"
    
### GE-SRTP

    "port:18245,18246 product:"general electric""
    
### MELSEC-Q

    "port:5006,5007 product:mitsubishi"
    
### CODESYS

    "port:2455 operating system"
    
### S7

    "port:102"
    
### BACnet

    "port:47808"
    
### HART-IP 

    "port:5094 hart-ip"
    
### ALETAS Omron

    "port:9600 response code"
    
### IEC 60870-5-104

    "port:2404 asdu address"
    
### DNP3

    "port:20000 source address"
    
### EtherNet/IP

    "port:44818"
    
### PCWorx

    "port:1962 PLC"
    
### Crimson v3.0

    "port:789 product:"Red Lion Controls"
    
### ProConOS

    "port:20547 PLC"  
    
## Escritorio remoto 

### VNC desprotegido 

    "authentication disabled" port:5900,5901
    "authentication disabled" "RFB 003.008"
    
### RDP de Windows
El 99,99 % está protegido por una pantalla secundaria de inicio de sesión de Windows

    "\x03\x00\x00\x0b\x06\xd0\x00\x00\x124\x00"
    
## Infraestructura de red 

### Routers hackeados
Routers que se comprometieron

    hacked-router-help-sos
    
### Instancias abiertas de Redis 

    product:"Redis key-value store"
    
### Citrix
Busque Citrix Gateway

    title:"citrix gateway"
    
### Weave Scope Dashboards
Acceso mediante línea de comandos dentro de pods de Kubernetes y contenedores Docker, y visualización/supervisión en tiempo real de toda la infraestructura

    title:"Weave Scope" http.favicon.hash:567176827
    
### MongoDB 
Las versiones anteriores eran inseguras por defecto. Muy atemorizante

    "MongoDB Server Information" port:27017 -authentication
    
### GUI web de Mongo Express
Como el infame phpMyAdmin pero para MongoDB

    "Set-Cookie: mongo-express=" "200 OK"
    
### Jenkins CI

    "X-Jenkins" "Set-Cookie: JSESSIONID" http.title:"Dashboard"
    
### Jenkins
Panel sin restricciones de Jenkins

    x-jenkins 200
    
### API de Docker

    "Docker Containers:" port:2375
    
### Registros privados de Docker 

    "Docker-Distribution-Api-Version: registry" "200 OK" -gitlab
    
### Servidores DNS abiertos Pi-hole 

    "dnsmasq-pi-hole" "Recursion: enabled"
    
### Iniciar sesión como root a través de Telnet

    "root@" port:23 -login -password -name -Session
    
### Acceso Telnet
NO se requiere contraseña para acceder a telnet

    port:23 console gateway

### Shell sin autenticación del sistema de videoconferencia de Polycom

    "polycom command shell"
    
### Dispositivos NPort serial-to-eth / MoCA sin contraseña 

    nport -keyin port:23
    
### Android Root Bridges
Un resultado tangencial del enfoque descuidado de actualización fracturada de Google

    "Android Debug Bridge" "Device" port:5555
    
### El adaptador de serie a Ethernet de Lantronix filtra las contraseñas de Telnet

    Lantronix password port:30718 -secured
    
### Aplicaciones virtuales de Citrix 

    "Citrix Applications:" port:1604
    
### Cisco Smart Install
Vulnerable (algo así como "por diseño", pero especialmente cuando está expuesto)

    "smart install client active"
    
### PBX IP Phone Gateways

    PBX "gateway console" -password port:23
    
### Videoconferencia de Polycom

    http.title:"- Polycom" "Server: lighttpd"
    "Polycom Command Shell" -failed port:23
    
### Configuración Telnet

    "Polycom Command Shell" -failed port:23
    
### Bomgar Help Desk Portal

    "Server: Bomgar" "200 OK"
    
### Intel Active Management CVE-2017-5689

    "Intel(R) Active Management Technology" port:623,664,16992,16993,16994,16995
    "Active Management Technology"
    
### HP iLO 4 CVE-2017-12542 

    HP-ILO-4 !"HP-ILO-4/2.53" !"HP-ILO-4/2.54" !"HP-ILO-4/2.55" !"HP-ILO-4/2.60" !"HP-ILO-4/2.61" !"HP-ILO-4/2.62" !"HP-iLO-4/2.70" port:1900
    
### Interfaz de administración del adaptador ethernet Lantronix sin contraseña

    "Press Enter for Setup Mode port:9999"
    
### Contraseñas Wi-Fi
Ayuda a encontrar las contraseñas wifi de texto claro en Shodan

    html:"def_wirelesspassword"
    
### Sitios de Wordpress mal configurados    
Si se accede a wp-config.php, se pueden proporcionar las credenciales de la base de datos

    http.html:"* The wp-config.php creation script uses this file"
    
## Acceso web de Outlook

### Exchange 2007

    "x-owa-version" "IE=EmulateIE7" "Server: Microsoft-IIS/7.0"
    
### Exchange 2010

    "x-owa-version" "IE=EmulateIE7" http.favicon.hash:442749392
    
### Exchange 2013 / 2016

    "X-AspNet-Version" http.title:"Outlook" -"x-owa-version"
    
### Lync / Skype for Business

    "X-MS-Server-Fqdn"
    
## Almacenamiento conectado a la red (NAS) 

### Recursos compartidos de archivos SMB (Samba)
Produce ~500,000 resultados... reduzca agregando "Documentos" o "Videos", etc

    "Authentication: disabled" port:445
    
### Específicamente Domain Controllers

    "Authentication: disabled" NETLOGON SYSVOL -unix port:445
    
### Recursos compartidos de red predeterminados de los archivos de QuickBooks

    "Authentication: disabled" "Shared this folder to access QuickBooks files OverNetwork" -unix port:445
    
### FTP Servers con login Anonymous habilitado

    "220" "230 Login successful." port:21
    
### Iomega / LenovoEMC NAS Drives

    "Set-Cookie: iomega=" -"manage/login.html" -http.title:"Log In"
    
### Buffalo TeraStation NAS Drives

    Redirecting sencha port:9000
    
### Logitech Media Servers

    "Server: Logitech Media Server" "200 OK"
    
### Plex Media Servers

    "X-Plex-Protocol" "200 OK" port:32400
    
### Tautulli / PlexPy Dashboards

    "CherryPy/5.1.0" "/home"
    
### Router doméstico conectado USB

    "IPC$ all storage devices"
    
## WebCams

### D-Link webcams

    "d-Link Internet Camera, 200 OK"
    
### Hipcam

    "Hipcam RealServer/V1.0"
    
### Yawcams

    "Server: yawcam" "Mime-Type: text/html"
    
### webcamXP/webcam7

    ("webcam 7" OR "webcamXP") http.component:"mootools" -401
    
### Android IP Webcam Server

    "Server: IP Webcam Server" "200 OK"
    
### Security DVRs

    html:"DVR_H264 ActiveX"
    
### Cámaras de vigilancia
Con usuario:admin y contraseña: :P 

    NETSurveillance uc-httpd
    Server: uc-httpd 1.0.0
    
## Impresoras y copiadoras

### Impresoras HP 

    "Serial Number:" "Built:" "Server: HP HTTP"
    
### Copiadoras/Impresoras Xerox 

    ssl:"Xerox Generic Root"
    
### Impresoras Epson 

    "SERVER: EPSON_Linux UPnP" "200 OK"
    "Server: EPSON-HTTP" "200 OK"
    
### Impresoras Canon 

    "Server: KS_HTTP" "200 OK"
    "Server: CANON HTTP Server"
    
## Dispositivos domésticos 

### Estéreos yamaha

    "Server: AV_Receiver" "HTTP/1.1 406"
    
### Apple AirPlay Receivers
Apple TVs, HomePods, etc

    "\x08_airplay" port:5353
    
### Chromecasts / Smart TVs

    "Chromecast:" port:8008
    
### Controladores de hogar inteligente Crestron

    "Model: PYNG-HUB"
    
## Cosas al azar 

### Controladores de impresora 3D OctoPrint 

    title:"OctoPrint" -title:"Login" http.favicon.hash:1307375944
    
### Etherium Miners

    "ETH - Total speed"
    
### Apache Directory Listings
Sustituya .pem con cualquier extensión o un nombre de archivo como phpinfo.php

    http.title:"Index of /" http.html:".pem"
    
### Muchos servidores de Minecraft 

    "Minecraft Server" "protocol 340" port:25565
    
### Literalmente todo en Corea del Norte 

    net:175.45.176.0/22,210.52.109.0/24,77.94.35.0/24
