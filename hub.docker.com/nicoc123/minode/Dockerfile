# Image Base
FROM node:latest

# Directorio de la APP
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependencias
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comandos
CMD ["npm", "start"]
