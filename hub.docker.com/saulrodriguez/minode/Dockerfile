# Imagen base
FROM node:latest

# Directorio de la app:
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependecias
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comando para ejecutar la aplicacion
CMD ["npm", "start"]
