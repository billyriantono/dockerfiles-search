#Imagen base
FROM node:latest

#Directorio de la aplicacion
WORKDIR /app

#Copia de archivos
ADD . /app

#Dependencias
RUN npm install

#Puerto de trabajo
EXPOSE 3000

#Comando requerido para ejecutarse
CMD ["npm", "start"]

#Version cambiada
