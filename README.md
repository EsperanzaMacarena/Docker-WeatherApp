# Docker--WeatherApp
Dockerización de una aplicación sobre datos meteorológicos en NodeJS y MongoDB.

## Pasos para dockerizar nuestra App NodeJs con MongoDB a través de Dockerfile

1. Debes crear una cuenta en mongoDB Atlas [mongoDB Atlas](https://www.mongodb.com/cloud/atlas) para alojar nuestra base de datos de forma remota. Para crear un clúster y conectar la base de datos con nuestra app NodeJS puedes seguir el siguiente [tutorial](https://codeforgeek.com/mongodb-atlas-node-js/)

2. Crea un Dockerfile en la raíz del proyecto e indica lo siguiente:

  a) La imagen que vamos a descargar para realizar la dockerización.
  
      FROM node:latest
     
      
  b) El directorio donde se alojará la app dentro de la imagen.
  
      WORKDIR /usr/src/app
      
  c) Instalamos las dependencias con el siguiente código:
     
      
      COPY package*.json ./
      
      RUN npm install
      
      
   d) Copiamos el código de nuestra app:
   
      COPY . .
      
   e) Indicamos el puerto en el que se expone nuestra app (en nuestro caso es el puerto 3000):
   
      EXPOSE 3000
   f) Finalizamos ejecutando el comando que arranca nuestra app:
   
      CMD [ "node", "./bin/www" ]
      
3. Creamos un fichero .dockerignore para poder obviar la carpeta node_modules y npm-debug.log
  ```
  node_modules
  npm-debug.log
  ```
  
 4. Creamos nuestra imagen contenida en el Dockerfile con el comando:
 `docker build -t <your username>/node-weather-app:1.0 .`
 
 5. Creamos un contenedor:
 `docker run --name weatherApp -p 8080:3000 -d <your username>/node-weather-app:1.0`
 
 6. Prueba la api con la url base: localhost:8080/api/
