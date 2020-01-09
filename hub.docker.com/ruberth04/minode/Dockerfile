#Imagen Base
FROM node:latest

#directorio de la app
WORKDIR /app

#copiado de archivos
ADD . /app

#devDependencies
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm", "start"]
