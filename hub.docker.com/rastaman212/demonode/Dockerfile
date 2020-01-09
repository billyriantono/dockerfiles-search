#imagen base
FROM node:latest

#Directorio de aplicación en el contenedor
WORKDIR /app

#Copiado de archivos para enviar al contenedor
ADD . /app

#Dependencias
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm","start"]
