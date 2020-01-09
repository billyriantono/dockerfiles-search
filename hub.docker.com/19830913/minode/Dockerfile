#Imagen base
FROM node:latest

#Directorio de la aplicación
WORKDIR /app

#Copiado de Archivos
ADD . /app

#Dependencias
RUN npm install

#Puerto que Expongo
EXPOSE 3000

# Comando para Ejecutar mi app
CMD ["npm","start"]
