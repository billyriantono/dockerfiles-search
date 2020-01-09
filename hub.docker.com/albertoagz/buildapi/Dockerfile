# Imagen raíz
FROM node
# Carpera raíz
WORKDIR /apitechu
# Copia de archivos
ADD . /apitechu
#Instalo los paquetes necesarios
RUN npm install
#Volumen de la imagen
VOLUME ["/log"]
# Puerto que expone
EXPOSE 3000
# Comando de iniciado
CMD ["npm", "start"]
