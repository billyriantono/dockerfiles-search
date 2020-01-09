# Imagen base
FROM node:latest

# Directorio de la app
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependencias - instala lo definido en package.json - solo para el docker build
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comandos
CMD ["npm", "start"]
