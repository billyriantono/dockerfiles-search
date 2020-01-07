FROM node:12.8.1-buster-slim

LABEL maintainer="Thiago Mota <tgmspawn@gmail.com>"
LABEL version="0.0.2"
LABEL title="Portinari Ionic Start Container"
LABEL description="Started Ionic project with Portinari UI"
LABEL vendor="http://portinari.io"

# Determina se vai iniciar o Ionic na abertura
ENV INIT_IONIC_SERVER=true
ENV INIT_IONIC_LAB=false

EXPOSE 8100
EXPOSE 8200

RUN apt update && \
    apt install -y yarn

RUN npm install -g @angular/cli
RUN npm install -g npm-add-script

RUN npm install -g ionic
RUN npm install -g cordova

WORKDIR /

RUN ionic start app blank --no-deps --no-confirm --no-git

WORKDIR /app

#TODO: Ajustar as dependências antes do NPM install
RUN npm install
RUN npm install @ionic/app-scripts@latest --save-dev
RUN npm install @portinari/portinari-sync --save
RUN ionic cordova plugin add cordova-plugin-network-information

# Depois de terminar de configurar, inserir o Script para o portinari
RUN npmAddScript -f -k ionicserve -v "ionic serve -b -p 8100 --address 0.0.0.0 --no-open"
RUN npmAddScript -f -k ioniclab -v "npm run ionicserve --lab"

# Guardo os arquivos gerados na pasta /template, exceto os node_modules
RUN mkdir /template/
RUN cp -rf `ls -A | grep -v "node_modules"` /template/

COPY ./start.sh /start.sh
CMD ["/start.sh"]
