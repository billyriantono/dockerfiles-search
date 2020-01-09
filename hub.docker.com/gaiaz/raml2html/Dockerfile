FROM node:lts-alpine

LABEL maintainer="Gaiaz Iusipov <g.iusipov@gmail.com>"

RUN set -xe \
    && yarn global add --silent \
        raml2html \
    && yarn cache clean --silent

WORKDIR /app

VOLUME /app

ENTRYPOINT ["raml2html"]

CMD ["--help"]
