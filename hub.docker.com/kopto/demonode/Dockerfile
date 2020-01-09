#Imagen base
FROM node:latest

#Directorios de la aplicacion en el contenedor
WORKDIR /app

#copiado de archivos
ADD . /app

#Dependencias
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm","start"]
