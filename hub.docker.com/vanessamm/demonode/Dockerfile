#Imagen bodyparser
FROM node:latest

#Directorio de la app en el contenedor
WORKDIR /app

#Copiado de archivos
ADD . /app
#añada todos los archivos de donde estoy parado al directorio raiz

#Dependencias (todas las dependencias deben estar en dependencies no en devDependencies, poner --Dependencies, si no se van a ir a devDependencies)
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando para ejecutar la aplicacion
CMD ["npm", "start"]
