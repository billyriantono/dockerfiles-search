FROM alpine:3.5

LABEL maintainer jerome masson <sphinxgaia@jeromemasson.fr>
LABEL description sample alpine

RUN apk add --update && apk add iputils

RUN mkdir -p /tmp/hello

WORKDIR /tmp/hello
COPY hlw.txt hlw.txt

RUN cat hlw.txt

CMD ["sh"]
