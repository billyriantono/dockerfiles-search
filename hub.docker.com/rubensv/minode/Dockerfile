#imagen base
FROM node:latest

#Directorio de la app
WORKDIR /app

#Archivos del contenedor
ADD . /app

#Dependencias
RUN npm install

#Puerto expuesto
EXPOSE 3000

#Comando
CMD ["npm", "start"]
