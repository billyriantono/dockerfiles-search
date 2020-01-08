FROM breauxaj/alpine:latest

RUN apk add nodejs npm yarn \
  && npm install -g \
    gulp-cli \
    typescript \
    webpack \
  && rm -rf /var/cache/apk/* \
  && mkdir -p /usr/src/app

WORKDIR /usr/src/app

VOLUME /usr/src/app

CMD ["sh"]

LABEL org.opencontainers.image.vendor="Breaux Heavy Industries" \
	org.opencontainers.image.url="https://breaux.io" \
	org.opencontainers.image.title="NodeJS" \
	org.opencontainers.image.description="NodeJS with Gulp, Typescript, Webpack and Yarn" \
	org.opencontainers.image.version="v0.0.1" \
	org.opencontainers.image.documentation="https://docs.breaux.io"