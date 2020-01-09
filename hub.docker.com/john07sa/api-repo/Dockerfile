#Imagen
#Imagen
FROM    node:slim
#Carpeta de la app
WORKDIR /miapp
#Copia archivos
ADD . /miapp
#Paquetes necesarios
RUN npm install
#Volumen 
#VOLUME /datos
#Puerto que expongo
EXPOSE 4000
#Comando de inicio
CMD ["npm", "start"]