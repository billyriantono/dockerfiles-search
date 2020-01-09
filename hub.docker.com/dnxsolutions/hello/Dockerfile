FROM alpine:3.8

RUN apk update && \
    apk add bash ca-certificates git openssl unzip wget make

WORKDIR /

COPY hello.sh /
COPY HELLO.md /

RUN chmod +x /hello.sh

CMD ["/hello.sh"]
