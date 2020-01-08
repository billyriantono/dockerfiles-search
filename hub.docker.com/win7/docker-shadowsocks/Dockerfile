FROM alpine:3.4

ENV DOCKERIZE_VERSION v0.3.0

ADD config.json.tmpl /etc/config.json.tmpl

RUN apk update && \
    apk add py-pip && \
    apk add build-base && \
    apk add wget && \
    pip install dumb-init  && \
    pip install shadowsocks

RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz --no-check-certificate \
    && tar -C /usr/local/bin -xzvf dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-alpine-linux-amd64-$DOCKERIZE_VERSION.tar.gz


ENTRYPOINT ["dumb-init", "--"]
CMD ["dockerize","-template","/etc/config.json.tmpl:/etc/config.json", "ssserver", "-c", "/etc/config.json"]
