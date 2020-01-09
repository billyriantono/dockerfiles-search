# Image base
FROM node:latest

#Directotio de la app en el contenedor
WORKDIR /app

#Copiado de archivos
ADD . /app

# Dependencias
RUN npm install

# Puerto que expongo (debe ser el mismo donde ejecutmaos la aplicacion)
EXPOSE 3000

#Comando de Docker de ejecucion de la aplicacion
CMD ["npm", "start"]
