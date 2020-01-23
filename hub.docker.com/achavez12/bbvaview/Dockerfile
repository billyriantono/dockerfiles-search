# Imagen base
FROM node:latest

# Directorio de la applicacion dentro del contenedor
WORKDIR /app

# Comidado de archivos
ADD build/default /app/build/default
ADD server.js /app
ADD package.json /app

# Dependencias
RUN npm install

# Puerto a ser expuesto
EXPOSE 8081

# COmando
CMD ["npm", "start"]
