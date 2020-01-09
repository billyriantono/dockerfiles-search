# Imagen docker base
FROM node:latest

# Directorio de trabajo de docker
WORKDIR /docker-api

# Copiar archivos del proyecto
ADD . /docker-api

# Environment Variables
ENV PORT 3000

# Instalar dependencias
RUN npm install

# Puerto donde exponemos contenedor
EXPOSE 3000
 
# Comando para lanzar la app
CMD ["npm", "start"]
