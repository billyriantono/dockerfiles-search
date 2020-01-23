# ESTE ES UN COMENTARIO
# PRIMERO VA LA IMAGEN BASE
FROM node:latest

# DIRECTORIO DE LA APP DENTRO DEL CONTENEDOR
WORKDIR /app

# COPIADO DE ARCHIVOS
ADD . /app

# CONFIGURACION DE HORA
RUN echo "America/Mexico_City" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

# DEPENDENCIA
RUN rm -rf node_modules/bcrypt
RUN npm install

# PUERTO
EXPOSE 3000

# COMANDO PARA EJECUTAR
CMD ["npm","start"]
