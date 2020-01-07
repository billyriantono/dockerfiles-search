# Image base
FROM node:latest

# Directorio de la app
WORKDIR /app

# Copiado de Archivos
ADD . /app
 
# Dependencias
RUN npm install

#Puerto que expongo
EXPOSE 3001

# Comandos
CMD ["npm", "start"]
