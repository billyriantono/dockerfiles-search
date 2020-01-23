# Imagen base
FROM node:latest

# Directorio de la app
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependencias
RUN npm install

# Puerto expuesto
EXPOSE 3000

# Comando para ejecutar la app
CMD ["npm", "start"]
