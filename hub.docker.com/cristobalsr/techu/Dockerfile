FROM node
WORKDIR /apitechu
ADD . /apitechu

#instalo paquetes necesarios
RUN npm install

# Volumen de la imagen
VOLUME ["/logs"]

EXPOSE 3000
CMD ["npm", "start"]
