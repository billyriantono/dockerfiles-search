# Imagen base
FROM node:latest

# Directorio de la aplicación dentro del contenedor
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependencias
RUN npm install

# Puerto que expongo
EXPOSE 3000

# No se requieren variables de entorno para esta API

# Comando
CMD ["npm", "start"]
