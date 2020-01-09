FROM alpine:3.5

LABEL maintainer jerome masson <sphinxgaia@jeromemasson.fr>
LABEL description sample hello world

RUN mkdir -p /tmp/hello

WORKDIR /tmp/hello
COPY hlw.txt hlw.txt

CMD cat hlw.txt
