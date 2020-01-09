# Imagen base
FROM node:latest

# Directorio de la applicacion dentro del contenedor
WORKDIR /app

# Comidado de archivos
ADD . /app

# Dependencias
RUN npm install

# Puerto a ser expuesto
EXPOSE 3000

# COmando
CMD ["npm", "start"]
