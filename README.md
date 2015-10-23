# Primer despliegue en OSE3

## Premisas
  1. Disponer de una VM o entorno local con docker instalado (v1.8 en mi caso)
  
  2. Configuración del docker daemon local para poder conectar con el registro de imagenes corporativas
     Hay que tener en cuenta dos temas:

      * Describir que el registro corporativo es inseguro puesto que ahora mismo se ha definido como tal 
      * Definir una excepción para que la ruta del registro corporativo no salga por el proxy)
  

## Procedimiento
  1. Descarga de imagenes docker necesarias a local desde el registro corporativo. De esta manera, se comprobará adicionalmente la conectividad. Comandos a ejecutar:

        `docker pull registry.lvtc.gsnet.corp/produban/redis:2.8`
        
        `docker pull registry.lvtc.gsnet.corp/produban/tomcat8:latest`
  
  2. En puesto local, UP de contenedores. Queda de manifiesto y tangible la necesidad de trabajar con dockers en puesto local con objeto de validar la aplicación y su configuración antes de subirla a OSE. 

  3. Redis   
   
        `docker run -d registry.lvtc.gsnet.corp/produban/redis:2.8 redis-server`  

  4. Tomcat con las variables de entorno que necesita la app (VARIABLES DE ENTORNO - CONFIGURACIÓN DE APLICACIONES COMO VARIABLES DE ENTORNO DESCARGADAS DE FORMA AUTOMATICA!!)
   
    `docker run -d -e REDIS_SERVICE_HOST="172.17.0.8" -e REDIS_SERVICE_PORT="6379" -p 8080:8080    registry.lvtc.gsnet.corp/produban/tomcat8:latest`
    
  5 Copiamos el fichero sobre el contenedor en ejecución (solo para testear rapidamente)
    `docker cp  httpsession-xml-0.0.1-SNAPSHOT.war NAMECONTAINER:/deployments/httpsession-xml-0.0.1-SNAPSHOT.war`
  
  6 Commit y (procedimiento poco ortodoxo - solo para testear rapidamente)
    `docker commit containerID urlregistry/user/nameimage:version`

    `docker push urlregistry/user/nameimage:version`
    
  7. Acceso a la APP (docker / docker-compose - up to you)
  ` curl namemachine:8080/httpsession-xml-0.0.1-SNAPSHOT/`

  4. Creacion de template OSE para el despliegue de la aplicación en OSE
  WTF!!
    La creación de la plantilla pasará por disponibilizar los siguientes elementos:
    1. 2 pods
    2. 2 servicios
    3. 1 route
    4. 2 deploymentConfig
    
   

  

