FROM node:8-alpine

RUN apk add --no-cache mongodb

VOLUME /data/db
EXPOSE 27017 28017

RUN npm install -g yarn

COPY run.sh /root
ENTRYPOINT [ "/root/run.sh" ]
