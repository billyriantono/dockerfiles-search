# Imagen raiz o de partida
FROM node
# Carpeta raiz desde la que queremos trabajar
WORKDIR /apitechu
# Copia de todos los archivos que haya en la carpeta donde está el fichero Dockerfile al directorio del docker
ADD . /apitechu
# Instalo los paquetes necesarios
RUN npm install
# Volumenes de la imagen
VOLUME ["/logs"]
# Puerto que expone
EXPOSE 3000
# Comando que se ejecuta al hacer docker run
CMD ["npm", "start"]
