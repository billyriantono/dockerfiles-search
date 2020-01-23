#Imagen base
FROM node:latest

#Directorio de la aplicación
WORKDIR /app

#Copiado de Archivos
ADD build/default /app/build/default
ADD server.js /app
ADD package.json /app

#Dependencias
RUN npm install

#Puerto que Expongo
EXPOSE 3000

# Comando para Ejecutar mi app
CMD ["npm","start"]
