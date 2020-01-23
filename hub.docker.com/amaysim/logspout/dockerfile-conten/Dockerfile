# Imagen body
FROM node:latest

# directorio de la app
WORKDIR /app

#copiado de Archivos
ADD . /app

#Dependecies
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm","start"]
