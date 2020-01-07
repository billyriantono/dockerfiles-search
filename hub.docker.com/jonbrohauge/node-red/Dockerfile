FROM node:6.9.5
MAINTAINER Jon Brohauge <jonbrohauge@gmail.com>
LABEL jonbrohauge.node-red.version="1.0.0-SNAPSHOT"

EXPOSE 1880

USER root
RUN npm install grunt-cli -g
RUN npm install -g --unsafe-perm node-red
RUN npm install grunt
CMD ["node-red"]
