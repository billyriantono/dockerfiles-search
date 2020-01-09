FROM node:10

# Create app directory
WORKDIR /usr/src/app


# Copia todos los archivos
COPY . ./

#Instala todas las dependencias
RUN npm install

#Se expone este porqu el frontend ya tiene el 4200
EXPOSE 4201

CMD [ "npm", "start" ]