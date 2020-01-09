# Imagen base
FROM node:latest

# Directorio de la app
WORKDIR /api

# Copio archivos
ADD . /api

# Dependencias
RUN npm install
#RUN apt-get update
#RUN apt-get install -y vim

# Puerto
EXPOSE 3000

# Comand
CMD ["npm", "start"]
