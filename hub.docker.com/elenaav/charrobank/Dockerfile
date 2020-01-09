# Imagen raiz
FROM node

# Carpeta raiz
WORKDIR /charrobank

# Copia de archivos de carpeta local a /charrobank
ADD . /charrobank

# Instalacion de las dependencias
RUN npm install --only=prod

# Puerto de trabajo
EXPOSE 3000

# Comando de inicializacion
CMD ["node", "server.js"]
