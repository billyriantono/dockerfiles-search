#Imagen Base
FROM node:latest

#directorio de la app
WORKDIR /app

#copiado de archivos
ADD build/default /app/build/default
ADD server.js /app
ADD package.json /app

#devDependencies
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm", "start"]
