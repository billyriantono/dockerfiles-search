#Imagen base
FROM node:latest

#Directorio de la app
WORKDIR /app

#Copiado de archivos
ADD build/default /app/build/default
ADD server.js /app
ADD package.json /app


#Depedencias
RUN npm install

#puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm", "start"]
