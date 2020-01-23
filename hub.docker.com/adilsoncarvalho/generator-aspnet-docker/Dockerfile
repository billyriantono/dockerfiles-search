FROM node:latest

LABEL maintainer "lc.adilson@gmail.com"

RUN mkdir -p /root/.config/configstore
RUN chmod g+rwx /root /root/.config /root/.config/configstore

RUN mkdir /var/stage && chmod g+rwx /var/stage
VOLUME /var/stage
WORKDIR /var/stage

RUN npm install -g bower yo generator-aspnet
RUN echo '{ "optOut": false }' > /root/.config/configstore/insight-yo.json

ENTRYPOINT ["yo", "aspnet"]
