FROM node:8.15.0-alpine

LABEL maintainer "etienne.chataignier@biig.fr"
RUN apk add --no-cache git

RUN npm install -g auto-changelog@1.11.0

ENV SRC_PATH /usr/local/src/your-app
RUN mkdir -p $SRC_PATH

VOLUME [ "$SRC_PATH" ]
WORKDIR $SRC_PATH

CMD ["--help"]
ENTRYPOINT ["auto-changelog"]
