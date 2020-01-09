# Imagen base
FROM node:latest

# Directorio de la app en el contenedor
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependencias
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comando con el que ejecutan Docker la aplicación
CMD ["npm", "start"]
