# Imagen origen
FROM node:6.0.0

# Carpeta raiz
WORKDIR /apitechu

# Copia de archivos de la carpeta local a apitechu (directorio de la imagen)
ADD . /apitechu

# Si en .Dokerignore añadimos ./node_modules
# poner esto:
RUN npm install

# Exponer puerto 3000 (que es el que estamos usando). Por defecto están todos cerrados.
EXPOSE 3000

# Comando de inicialización
CMD ["npm", "start"]
