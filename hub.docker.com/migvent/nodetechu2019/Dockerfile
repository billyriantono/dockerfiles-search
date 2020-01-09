# Imagen base
FROM node:latest

# Directorio de la app
WORKDIR /app

#Copiado de archivos (copiar lo q tengo en raiz al directorio raiz del contenedor docker)
ADD . /app

#Dependencies
RUN npm install

#Puerto que expongo
EXPOSE 3001

#Comando
CMD ["npm","start"]
