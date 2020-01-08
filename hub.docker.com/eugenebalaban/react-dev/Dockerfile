FROM node:6-alpine

RUN apk add --update git python build-base curl bash \
	&& curl -Ls "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C / \
	&& apk del git python build-base curl \
    &&  rm -rf /usr/share/man /tmp/* /var/tmp/* /var/cache/apk/*

WORKDIR /usr/src/app

EXPOSE 8000

CMD ["npm", "start"]