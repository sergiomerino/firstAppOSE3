# Desplegando la primera aplicacion en OSE3

## Premisas
  1. Disponer de una VM o entorno local con docker instalado (v1.8)
  
  2. Configuración del docker daemon local para poder conectar con el registro de imagenes corporativas
     bla bla bla bla
  
## Procedimiento
  1. Descarga de imagenes docker necesarias a local desde el registro corporativo. De esta manera, se comprobará adicionalmente la conectividad. Comandos a ejecutar:

  `docker pull registry.lvtc.gsnet.corp/produban/redis:2.8 `
  `docker pull registry.lvtc.gsnet.corp/produban/tomcat8:latest`
  
  2. Up de contenedores. 
  2.1 Redis   
    `docker run -d registry.lvtc.gsnet.corp/produban/redis:2.8 redis-server`  

  2.2 Tomcat con las variables de entorno que necesita la app
    `docker run -d -e REDIS_SERVICE_HOST="172.17.0.8" -e REDIS_SERVICE_PORT="6379" -p 8080:8080    registry.lvtc.gsnet.corp/produban/tomcat8:latest`
    
  2.3 Copiamos el fichero sobre el contenedor en ejecución (solo para testear rapidamente)
    `docker cp  httpsession-xml-0.0.1-SNAPSHOT.war NAMECONTAINER:/deployments/httpsession-xml-0.0.1-SNAPSHOT.war`
    
  3. Testing en local (docker / docker-compose - up to you)
  ` curl namemachine:8080/XXXX`

  4. Creacion de template OSE para el despliegue de la aplicación en OSE
  WTF!!
    La creación de la plantilla pasa por disponibilizar los siguientes elementos:
    1. 2 pods
    2. 2 servicios
    3. 1 route
    4. 1 deploymentConfig
    5. Escribir un json 
   

  
## Procedimiento
