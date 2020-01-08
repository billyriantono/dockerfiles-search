FROM alpine
MAINTAINER Angeiv Zhang <angeiv.zhang@gmail.com>

RUN apk --update add nodejs nodejs-npm \
    && rm -rf /var/cache/apk/*

LABEL version="4.0.0-alpha.6"

RUN npm install -g gitbook-cli && gitbook fetch ${version} \
    && npm cache clear \
    && rm -rf /tmp/*


WORKDIR /srv/gitbook

VOLUME /srv/gitbook /srv/html

EXPOSE 4000 35729

CMD ["gitbook", "serve"]
