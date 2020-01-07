# Imagen origen
#FROM node:8.12.0
FROM node:8.12.0-alpine

# Carpeta raiz
WORKDIR /node-miner

# Copia archivos de carpeta local a node-bank
ADD . /node-miner

# si .dockerignore  añadir /node_modules
RUN npm install

# Exponer puerto
EXPOSE 3001 6001

# Comando inicializacion
CMD ["npm", "start"]