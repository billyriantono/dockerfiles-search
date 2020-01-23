FROM nodered/node-red-docker:slim
Maintainer andre@jeanmaire.nl

USER root
RUN apk add --no-cache openssl python2 py-pip nano

RUN npm install node-red-dashboard
RUN npm install node-red-contrib-opcua
RUN npm install simpletime
RUN npm install bcryptjs
RUN npm install -g node-red-admin

RUN npm uninstall -g node-red-pi

RUN pip install --upgrade pip
RUN pip install pyro
RUN mkdir /opc

COPY opc/* /opc/
