# Imagen base
FROM node:latest

# Directorio de la app en el contenedor
WORKDIR /app

# Copiado de archivos de la release y los necesarios que no toma de la release
ADD /build/default /app/build/default
ADD server.js /app
ADD package.json /app

# Dependencias
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comando con el que ejecutan Docker la aplicación
CMD ["npm", "start"]
