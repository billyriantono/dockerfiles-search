FROM keymetrics/pm2-docker-alpine:latest
WORKDIR /root
RUN apk update && \
    apk upgrade && \
    apk add git
ENV HOME /root  
COPY bower.json ./
COPY index.html ./
COPY keythereum.min.js ./
COPY socket.io.js ./
COPY manifest.json ./
COPY package.json ./
COPY polymer.json ./
COPY server.js ./
RUN npm install
RUN npm install -g bower
RUN bower install --allow-root 

COPY images ./images/
COPY src ./src/
COPY test ./test/

RUN npm install -g polymer-cli --unsafe-perm=true
RUN polymer build

COPY pm2.json ./
EXPOSE 8080
CMD [ "pm2-docker", "start", "pm2.json" ]