FROM node:10.9-alpine
#FROM node:7.0.5-alpine

USER 0
WORKDIR /opt

RUN apk --no-cache add --virtual native-deps \
  g++ gcc libgcc libstdc++ linux-headers autoconf automake make nasm python git && \
  npm i -g phantomjs-prebuilt --unsafe-perm --silent \
  npm install --quiet node-gyp -g \
  npm install --quiet spectacle-docs@1.0.5 -g

RUN apk del native-deps

RUN apk update \
	&& apk add git vim curl wget bash \
   && rm -rf /var/cache/apk/* 

COPY entrypoint.sh entrypoint.sh
RUN mkdir -p /opt/public/images
COPY is_logo.svg /opt/public/images

ENTRYPOINT ["/opt/entrypoint.sh"]
