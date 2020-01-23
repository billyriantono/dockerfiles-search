# Imagen origen
FROM node:6.0.0

# Carpeta raíz
WORKDIR /apitechu

# Copia de archivos de la carpeta local a apitechu
ADD . /apitechu

# RUN se ejecuta en el proceso de construcción de la imagen
RUN npm install

# Exponer puerto
EXPOSE 3000

# Comando de inicialización. CMD se ejecuta en el proceso de ejecución de la imagen (no en construcción como hace el comando RUN)
CMD ["npm","start"]
