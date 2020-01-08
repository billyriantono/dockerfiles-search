FROM node:8-alpine

LABEL maintainer "martijn.pepping@automiq.nl"

RUN addgroup sqlectron -S && \
    adduser sqlectron -G sqlectron -S && \
    mkdir -p /home/sqlectron/.config/Sqlectron && \
    apk update && \
    apk add git vim nano && \
    rm -rf /var/cache/apk/* && \
    npm install -g sqlectron-term

USER sqlectron
ENTRYPOINT [ "/usr/local/bin/sqlectron-term" ]
