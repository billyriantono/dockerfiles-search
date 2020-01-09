FROM alpine:edge

MAINTAINER Thierry Sallé (@tsalle)

ENV RIEMANN_VERSION 0.2.14

RUN apk --update upgrade && \
    apk add openjdk8 \
            bash \
            wget


RUN mkdir /app && \
    cd /app && \
    wget https://github.com/riemann/riemann/releases/download/0.2.14/riemann-$RIEMANN_VERSION.tar.bz2 && \
    bunzip2 riemann-0.2.14.tar.bz2 && \
    tar -xf riemann-0.2.14.tar && \
    rm -f riemann-0.2.14.tar && \
    apk del wget

WORKDIR /app/riemann-0.2.14

RUN sed -i "s/127.0.0.1/0.0.0.0/g" /app/riemann-0.2.14/etc/riemann.config

EXPOSE 5555/tcp 5555/udp 5556

CMD ["/app/riemann-0.2.14/bin/riemann"]
