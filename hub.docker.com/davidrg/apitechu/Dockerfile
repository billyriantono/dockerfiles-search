# Imagen origen

FROM node

# Carpeta raiz
WORKDIR /apitechu

# Copia de archivos
ADD . /apitechu

# Instalar dependencias
RUN npm install

# Exponer puerto
EXPOSE 3000

# Comando de inicio
CMD ["npm", "start"]
