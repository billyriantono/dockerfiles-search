#imagen origen de contenedor
FROM node

#Carpeta raiz
WORKDIR /apitechu

#Copia de archivos de local al contenedor
ADD . /apitechu

#actualizar librerias
RUN npm install

#Exponer puertos del contenedor
EXPOSE 3000

#Comando de inicio de la APP
CMD [ "npm","start" ]
