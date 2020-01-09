#Nombre del archivo va con mayúscula
#Imagen base
FROM node:latest

#Directorio de la app en el contenedor
WORKDIR /app

#Copiado de archivos  el punto se refiere a todos los archivos
ADD . /app

#Dependencias que tenemos definidas en este caso  JSON
RUN npm install

#Puerto que expongo debe ser el mismo  con que corre la aplicación
EXPOSE 3000

#Comando necesario para ejecutar la aplicación
CMD ["npm", "start"]
