# Image base
From node:latest

# directorio de la app en el contenedor
WORKDIR /app

# Copiado de archivos
ADD . /app

# Dependencias
RUN npm install

# Puerto que expongo
EXPOSE 3000

# Comando
CMD ["npm", "start"]
