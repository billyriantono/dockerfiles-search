# Imagen raíz
FROM node
# Directorio raíz
WORKDIR /apitechu
# Copia de archivos
ADD . /apitechu
# Instala paquetes necesarios
RUN npm install
# Volumen de la Imagen
VOLUME ["/logs"]
# Puerto que expone
EXPOSE 3000
# Comando de iniciado
CMD ["npm", "start"]
