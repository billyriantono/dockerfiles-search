#Imagen base
FROM node:latest

#directorio donde van a estor nuestros ficheros
#Directorio de la app
WORKDIR /app


#Copiado de archivos
#que todo lo de la raiz lo copie en el contenedor /app es la raiz del contenedor
ADD build/default /app/build/default
#ARCHIVOS NECESARIOS DE RAPID DE NODE
ADD server.js /app
ADD package.json /app


#Dependencias
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm", "start"]
