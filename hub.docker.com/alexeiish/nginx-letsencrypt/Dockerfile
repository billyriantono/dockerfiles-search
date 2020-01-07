FROM nginx:1.15.2-alpine
LABEL maintainer="Alex Shvedov <alexeii.shvedov@gmail.com>"

ENV UID=nginx \
    GUID=nginx

RUN set -ex \
    # for ps -p
    && apk add --no-cache procps \
    && apk add --no-cache certbot


RUN set -ex \
    && mkdir -p /etc/letsencrypt \
    && chown -R $UID:$GUID /etc/letsencrypt \
    && mkdir /app \
     && chown -R $UID:$GUID /app

COPY ./scripts/ /scripts

RUN chmod +x /scripts/*.sh
COPY ./conf/ /etc/nginx/conf.d

ENTRYPOINT ["/scripts/entrypoint.sh"]
WORKDIR /app
VOLUME ["/etc/letsencrypt"]
