#Imagen de la que parto
FROM node:boron
#Carpeta de la app
WORKDIR /miapp
#Copia archivos
ADD . /miapp
#Paquetes necesarios
RUN npm install
#Puerto que expongo
EXPOSE 3000
#Comando de inicio
CMD ["npm", "start"]
