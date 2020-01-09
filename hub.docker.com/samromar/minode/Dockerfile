# Image base
FROM node:latest

# Directorio de la app en el contenedor
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependecias
RUN npm install

# Puerto que expongo
EXPOSE 3000

#Comando
CMD ["npm","start"]
