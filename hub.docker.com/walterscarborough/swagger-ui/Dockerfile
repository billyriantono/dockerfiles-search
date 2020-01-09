FROM alpine:3.3

MAINTAINER Walter Scarborough <walter.scarborough@gmail.com>

ENV SWAGGERUI_VERSION=2.1.3

RUN apk add --update \
    curl \
    nginx \
    zip \

    && \

    curl -L https://github.com/swagger-api/swagger-ui/archive/v$SWAGGERUI_VERSION.zip >> /root/$SWAGGERUI_VERSION.zip \
    && cd /root && unzip /root/$SWAGGERUI_VERSION \
    && mv /root/swagger-ui-$SWAGGERUI_VERSION/dist /swagger-ui \
    && rm -R /root/swagger-ui-$SWAGGERUI_VERSION \
    && rm /root/$SWAGGERUI_VERSION.zip \

    && \

    apk del \
    curl \
    zip \

    && \

    rm -rf /var/cache/apk/* \

    && mkdir /etc/nginx/sites-available \
    && mkdir /etc/nginx/sites-enabled

# NGINX Setup
COPY docker/nginx/nginx.conf /etc/nginx/nginx.conf
COPY docker/nginx/swagger-ui /etc/nginx/sites-enabled/

CMD /usr/sbin/nginx -g "daemon off;"

EXPOSE 3000
