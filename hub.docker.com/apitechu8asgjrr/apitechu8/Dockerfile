# Imagen base
FROM node

# Carpeta trabajo
WORKDIR /apitechu

# Copiamos el fichero de dependencias
COPY package*.json ./

# Instalamos los paquetes necesarios
RUN npm install -g polymer-cli --unsafe-perm
RUN npm install -g bower --unsafe-perm
RUN npm install --production

# Instalamos los paquetes de bower
COPY bower.json ./
RUN bower install --allow-root

# Añadimos los archivos de la app
ADD . /apitechu

# Construimos el front
RUN npm run front

# Abrimos el puerto de la API
EXPOSE 3000

# Comando de inicializacion
CMD ["npm", "start"]