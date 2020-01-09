# Imagen base
FROM node:latest

# Directorio de la app en el contenedor
WORKDIR /app

#Copiado de achivos
ADD . /app

#Dependencias
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando para ejecutar en docker
CMD ["npm", "start"]