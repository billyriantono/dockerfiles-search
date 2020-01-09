#image base
FROM node:latest
#Directorio
WORKDIR /app
#Copiado de archivos
ADD . /app
#Dependencias
RUN npm install
#Puerto
EXPOSE 3000
#Comando
CMD ["npm","start"]
