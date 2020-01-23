#Imagen base
FROM node:latest

#Directorio de la app en el contenedor
WORKDIR /app

#Copiado de archivos
ADD . /app

#Dependencias
RUN npm install

#Puesto que expongo
EXPOSE 3000

#Comando
CMD ["npm", "start"]
