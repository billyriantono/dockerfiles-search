#Imagen base
FROM node:latest

#Directorio de la app en el contenedor (dir raiz)
WORKDIR /app

#Copiado de archivos todos a /app
ADD /build/default /app/build/default
ADD server.js /app
ADD package.json /app

#Dependencias
RUN npm install

#Puerto a exponer MISMO de la aplicación definido en server.js
EXPOSE 8081

#Comando a ejecutar
CMD ["npm", "start"]
