#Imagen base
FROM node:latest

#Directorio de la app
WORKDIR /app

#Copiado de archivos
ADD build/default /app/build/default
ADD server.js /app
ADD package.json /app

#Dependencias
RUN npm install

#Puerto expuesto
EXPOSE 3000

#Comando de ejecucion
CMD ["npm", "start"]
