# Imagen origen
# Si no se indica la version, por defecto coge "latest"
FROM node

# Carpeta raiz que vamos a tener en el docker
WORKDIR /apitechu

# Copiamos el codigo fuente de nuestra carpeta local (en la que esta el dockerfile,
# por eso especificamos .) al directorio raiz de la imagen (que le hemos indicado
# anteriormente)
ADD . /apitechu

# Como hemos metido el ./node_modules en el .dockerignore para que no lo copie (es lo suyo), hay que
# indicarle que lo instale al construir el docker porque no va a estar
RUN npm install

# Exponer puerto
EXPOSE 3000

# Comando de inicializacion de la api
CMD ["npm", "start"]
