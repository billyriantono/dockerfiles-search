#Imagen base
FROM node:latest

# Directorio de la aplicación
WORKDIR /app

# Copiado de la aplicación
ADD . /app

# Copiado de dependencias
RUN npm install
RUN apt-get update
RUN apt-get install -y vim

# Puerto a publicar
EXPOSE 3000

# Comando a ejecutar
CMD ["npm", "start"]
