# Imagen Raíz
FROM node
# Carpeta Raíz
WORKDIR /apitechu
# Copia de archivos
ADD . /apitechu
# instalar los paquetes necesarios
RUN npm install
# Volumen de la imagen
VOLUME ["/logs"]
# Puerto que expone
EXPOSE 3000
# Comando de arranque
CMD ["npm", "start"]
