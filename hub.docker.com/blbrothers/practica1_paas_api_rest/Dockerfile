# Imagen raíz, node es con lo que estamos generando nuestro paquete ejecutable
FROM node

# Carpeta raíz donde meteremos todo lo necesario
WORKDIR /apitechu

# Copia de archivos desde donde estoy a la carpeta creada
ADD . /apitechu

# Añadimos volumen
# VOLUMEN ['/LOGS']

# Exponer el puerto
EXPOSE 3000

# Instalar dependencias
# RUN npm install

# Comando de inicializar
CMD ["npm", "start"]
