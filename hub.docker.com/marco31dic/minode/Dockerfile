# Imagen base
FROM node:latest

# Directorio de la app
WORKDIR /app

#Copiado de archivos de mi raiz
ADD . /app

#Dependencias para ejecutar (se instala todo)
RUN npm install

#Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm","start"]
