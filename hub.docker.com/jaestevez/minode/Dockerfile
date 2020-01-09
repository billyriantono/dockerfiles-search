#Imagen base
FROM node:latest
#Directorio de la app
WORKDIR /app
#Copiar archivos
ADD . /app
#Dependencias
RUN npm install
# puertos
EXPOSE 3000
# comando
CMD ["npm", "start"]