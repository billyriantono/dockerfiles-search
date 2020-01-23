#Imagen origen
FROM node:6.0.0

#Carpeta raíz donde se van a ejecutar los comandos a continuación
WORKDIR /apitechu

# Copia de archivos de la carpeta local a apitechu
ADD . /apitechu

#RUN se ejecuta en el proceso de creación de la imagen
#Si en .dockerignore añadimos ./node_modelues hay que ejecutar los siguiente
RUN npm install

# Exponer puerto
EXPOSE 3000

#Comando de inicialización
#CMD es en ejecución de la instancia, se ejecuta una vez construida la imagen y cuando se va a ejecutar el contenedor
CMD ["npm", "start"]
