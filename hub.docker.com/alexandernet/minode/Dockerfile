# definir imagen base de la que vamos a partir
FROM node:latest

# Directorio de la app en el contenedor
WORKDIR /app

#copiado de archivos
ADD . /app

# Dependencias. que cuando se cree la imagen descargue todas las dependencias
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando con el que debe ejecutar docker nuestra aplicacion
CMD ["npm", "start"]
