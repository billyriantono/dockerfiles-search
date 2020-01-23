FROM node:13.6.0-alpine3.10
LABEL maintainer "Lorenzo Gigli <lorenzo.dramis@gmail.com>"

RUN apk add --no-cache \
    ca-certificates \
	gcc \
	git \
	make \
    python2

ENV NODEWOT_VERSION v0.7.0-SNAPSHOT.4

RUN git clone --depth 1 --branch "${NODEWOT_VERSION}" https://github.com/eclipse/thingweb.node-wot.git /node-wot

RUN cd node-wot \
    && npm install \
    && npm run build \
    && npm run link

EXPOSE 8080

WORKDIR /home/node

ENTRYPOINT [ "wot-servient" ]