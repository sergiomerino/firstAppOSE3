# Desplegando la primera aplicacion en OSE3

## Premisas
  1. Disponer de una VM o entorno local con docker instalado (v1.8)
  2. Configuración del docker daemon local para poder conectar con el registro de imagenes corporativas
  
## Procedimiento
  1. Descarga de imagenes docker necesarias a local desde el registro corporativo. De esta manera, se comprobará adicionalmente
  la conectividad. Comandos a ejecutar:

  `docker pull registry.lvtc.gsnet.corp/produban/redis:2.8 redis-server`
  `docker pull registry.lvtc.gsnet.corp/produban/tomcat8:latest`
  
  2. Up de contenedores. 
  3. Redis   
    `docker run -d registry.lvtc.gsnet.corp/produban/redis:2.8 redis-server`  
  4. Tomcat con la aplicacion embebida   
    `docker run -d registry.lvtc.gsnet.corp/produban/tomcat8:latest -link `  
   
  
  4. Testing en local (docker / docker-compose - up to you)
  4. Creacion de template OSE para el despliegue de la aplicación en OSE
  
## Procedimiento
