# Imagen base 
FROM node:latest

# Directorio de la app
WORKDIR /Users/johnlopezvega/Documents/appdocker

# Copiado de archivos
ADD . /Users/johnlopezvega/Documents/appdocker

# Dependencias
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comando
CMD [ "npm", "start" ]