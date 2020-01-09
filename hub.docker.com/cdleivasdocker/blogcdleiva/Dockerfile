# Para aprovechar la plantilla existente en hub.docker.com que instala Node y NPM
FROM node:boron

# Crear directorio de la app
RUN mkdir -p /usr/src/app
# Indicar la carpeta de trabajo
WORKDIR /usr/src/app

# Instalar dependencias
COPY package.json /usr/src/app
RUN npm install

# Empaquetar código
COPY . /usr/src/app

# Exponer el puerto
EXPOSE 8081
# CMD lanza el motor de Docker. Sólo hay una, mientras que RUN puede haber varias
# Ojo a los espacios
CMD [ "npm", "start" ]
