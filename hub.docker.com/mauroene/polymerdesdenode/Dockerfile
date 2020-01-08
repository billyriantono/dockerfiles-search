# Imagen Base
FROM node:latest

# Directorio de la app
WORKDIR /app

# Comentario de archivos
# Añade todo los archivos de la raíz
ADD build/default /app/build/default
ADD server.js /app
ADD package.json /app

# Dependencias
RUN npm install

#Puerto que expongo
EXPOSE 3000

# Comando
CMD ["npm", "start"]
