# Imagen base para partir
FROM node:latest

# Directorio de la app en el contenedor
WORKDIR /app

#copiado de archivos  del directorio actual al raiz del contenedor
ADD . /app

#   Dependencias
RUN npm install

#   Puerto expuesto
EXPOSE 3000

#   Comando para ejecutar la app docker
CMD [ "npm","start" ]