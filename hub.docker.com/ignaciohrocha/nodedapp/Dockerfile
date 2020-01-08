#Imagen base:
FROM node:slim

#Directorio de la aplicacion
WORKDIR /app

#Archivos a copiar
ADD app /app/app
ADD index.js /app
ADD package.json /app

#Comando a correr
RUN npm install

#Puesto expuesto
EXPOSE 80

#Comando de ejecucion
CMD ["npm", "start"]
