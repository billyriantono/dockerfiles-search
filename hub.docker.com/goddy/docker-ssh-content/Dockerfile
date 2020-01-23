FROM ubuntu:latest

LABEL maintainer = "Oscar Bocanegra oscargiovanni@gmail.com - German Medina gd.medinan@gmail.com"

ENV IONIC_VERSION=4.10.3 \
    CORDOVA_VERSION=8.1.2 \
    NPM_VERSION=6.4.1 \
    NODE_VERSION=10.15.0 

# Install basics
RUN apt-get update; \
    apt-get install -y npm; \
    apt-get install -y nodejs; \
    apt-get install -y git; 

# Install Product Ionic - cordova
RUN npm install -g cordova@"$CORDOVA_VERSION"; \
    npm install -g ionic@"$IONIC_VERSION"; \
    npm install --save node-sass; \
    npm cache clear --force;

# Creacion de carpeta myApp en la imagen
RUN mkdir myApp

# Creacion de proyecto myApp en la imagen
#RUN ionic start myApp sidemenu

# Montaje de volumen myApp
VOLUME ["/myApp"]

# Direccionamiento a carpeta myApp
WORKDIR /myApp
EXPOSE 8100 8200 22

#CMD ["/bin/bash"]
CMD ["ionic", "serve"]