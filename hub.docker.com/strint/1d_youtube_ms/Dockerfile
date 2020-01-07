#imagen desde la cual crearemos la nuestra
FROM node:8.11.1
 
WORKDIR /src 
#copiamos los archivos a nuestro directorio /src
COPY index.js /src/index.js
COPY package.json /src/package.json

COPY . /src
#instalamos los modulos
RUN cd /src
RUN npm cache clean -f
RUN npm install -g
#puerto que va a exponer nuestra imagen Docker
EXPOSE 8002
 
#ejecutamos nuestro servidor
CMD ["node", "/src/index.js"]