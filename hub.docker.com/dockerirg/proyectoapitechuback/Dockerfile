# Imagen raiz
FROM node

#Carpeta raiz
WORKDIR /apitechu

# Copia de archivos
ADD . /apitechu

# Exponer puerto
EXPOSE 3000

#Instalar dependencias
RUN npm install bcrypt
RUN npm install

# Comando de inicialización
CMD ["npm","start"]
