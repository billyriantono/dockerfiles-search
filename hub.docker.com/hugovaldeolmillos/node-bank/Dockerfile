# Imagen origen
FROM node:8.12.0

# Carpeta raiz
WORKDIR /node-bank

# Copia archivos de carpeta local a node-bank
ADD . /node-bank

# si .dockerignore  añadir /node_modules
RUN npm install

# Exponer puerto
EXPOSE 3001 6001

# Comando inicializacion
CMD ["npm", "start"]
