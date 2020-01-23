# Imagen origen, por defecto "latest"
FROM node

# Carpeta raiz en el docker
WORKDIR /blockbank

# Copia el codigo fuente de nuestra carpeta local al directorio raiz de la imagen
# anteriormente)
ADD . /blockbank

RUN npm install

# Exponemos el puerto
EXPOSE 3003

# Comando de inicializacion de la api
CMD ["npm", "start"]
