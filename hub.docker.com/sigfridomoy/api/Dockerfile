##Imagen de la que parto
FROM node:slim
##Directorio de trabajo
WORKDIR /api
##Copia archivos
ADD . /api
##Paquetes necesarios
RUN npm install
##Puerto en que expongo
EXPOSE 3000
##Comando de inicio
CMD ["npm", "start"]