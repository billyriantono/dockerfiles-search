# Imagen base
FROM node:latest

# Directorio de la APP
WORKDIR /app

# Copiado de Archivos
ADD . /app

# Dependencies
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comando
CMD ["npm","start"]
