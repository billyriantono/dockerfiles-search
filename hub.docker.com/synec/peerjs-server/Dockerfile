FROM node:10-alpine
LABEL maintainer="Daniel Grabert <dg@indivirtuell.net>"

RUN apk update && apk upgrade

RUN npm -g install peer

ENTRYPOINT peerjs --port ${PEERJS_PORT:-3333} --key ${PEERJS_KEY:-peerjs}
