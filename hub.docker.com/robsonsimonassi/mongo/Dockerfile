FROM alpine:edge

MAINTAINER robson.simonassi@sciensa.com

RUN apk update && apk add --no-cache mongodb

EXPOSE 27017 27017

VOLUME /data/db

WORKDIR /

ADD start.sh           start.sh
ADD configure-mongo.sh configure-mongo.sh

RUN chmod +x start.sh
RUN chmod +x configure-mongo.sh


CMD ["/start.sh"]