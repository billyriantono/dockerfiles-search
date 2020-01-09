# Imagen base
FROM node:latest

# Directorio de aplicación dentro del contenedor
WORKDIR /app

# Copiado de archivos (se copian todos los archivos desde donde estamos hacia el dir de la app
ADD . /app

# Dependencias (RUN npm install: para que cada ves que se haga un pull se reinstale)
# y va ligado contra el archivo packege.json apartado dependencies
RUN npm install

# Puerto en el que corre la aplicación
EXPOSE 3000

# Comando (para ejecutar la app)
# y va ligado contra el archivo packege.json apartado start
CMD ["npm","start"]
