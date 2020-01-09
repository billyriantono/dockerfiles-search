#Imagen base
FROM node:latest

#Directorio de la app
WORKDIR /app

#Copiado de Archivos
ADD . /app

#Dependencias
RUN npm install

#Puerto a aperturar
EXPOSE 3000

#Comando
CMD ["npm", "start"]
