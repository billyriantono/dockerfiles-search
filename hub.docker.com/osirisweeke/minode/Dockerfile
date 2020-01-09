# Imagen base
From node:latest

# Directorio de la app en el contenedor
WORKDIR /app

# Copiado de archivos, con ADD . decimos que enviamos todos los archivos a ese directorio
ADD . /app

# Dependencias
RUN npm install

# Puerto que se expone
EXPOSE 3000

#Comando con el que debe ejecutar docker nuestra aplicacion
CMD ["npm","start"]
