FROM node:10

# Creamos el directorio de la aplicacion Node - Holcim usuarios
WORKDIR /usr/src/app

# Aseguramos que se copian tanto el package.json como package-lock.json
COPY package*.json ./

# Instalamos las dependencias
RUN npm install

# Copiamos la aplicacion completa
COPY . .

# Exponemos el puerto 3000
EXPOSE 3000

# Ejecutamos la aplicacion en el contenedor
CMD [ "node", "server.js" ]
