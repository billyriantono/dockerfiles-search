FROM node:lts-alpine

LABEL maintainer="Gaiaz Iusipov <g.iusipov@gmail.com>"

RUN set -xe \
    && yarn global add --silent \
        yaspeller \
    && yarn cache clean --silent

WORKDIR /app

VOLUME /app

ENTRYPOINT ["yaspeller"]

CMD ["--help"]
