FROM python:alpine

RUN apk add --no-cache git transmission-cli

WORKDIR /workdir

COPY tremc /workdir/tremc

ENTRYPOINT ["/workdir/tremc"]
