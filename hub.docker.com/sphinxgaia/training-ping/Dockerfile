FROM alpine:3.5

LABEL maintainer jerome masson <sphinxgaia@jeromemasson.fr>
LABEL description sample ping

RUN apk add --update && apk add iputils

RUN mkdir -p /tmp/hello

WORKDIR /tmp/hello
COPY hlw.txt hlw.txt

RUN cat hlw.txt

COPY ./docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["docker-entrpoint.sh"]

CMD ["127.0.0.1"]
