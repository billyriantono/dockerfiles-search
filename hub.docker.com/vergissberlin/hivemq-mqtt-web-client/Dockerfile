FROM nginx:alpine

WORKDIR /var/www/

RUN apk add --update \
    && rm -rf /var/cache/apk/* \
    && wget https://github.com/hivemq/hivemq-mqtt-web-client/archive/master.zip \
    && unzip master.zip \
    && mv hivemq-mqtt-web-client-master html\
    && rm master.zip

ADD setup /

EXPOSE 80

CMD ["nginx"]
