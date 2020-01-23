#Imagen base
FROM node:latest

#Directorio de la aplicacion del contenedor
WORKDIR /app

#Copiado de archivos (anadir todos los archivos del directorio actual al directorio app)
ADD . /app

#Dependencias
#RUN npm install

#Puerto que expongo (el mismo que ejecuta la aplicacion)
EXPOSE 3000

#Comando
CMD ["npm", "start"]
