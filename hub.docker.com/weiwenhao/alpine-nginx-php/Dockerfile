FROM weiwenhao/php:latest

LABEL maintainer="weiwenhao <coder@weiwenhao.com>"

RUN apk add --update nginx \
    && rm -rf /var/cache/apk/*

ADD root / 

EXPOSE 80 443

WORKDIR /code

ENTRYPOINT ["/start.sh"]