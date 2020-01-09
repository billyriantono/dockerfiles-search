ARG ALPINE_VERSION=3.10

FROM alpine:${ALPINE_VERSION} as build

ARG WEBMAN_VERSION=1.47.23

ENV WEBMAN_VERSION=$WEBMAN_VERSION

LABEL webman.version=$WEBMAN_VERSION

RUN apk add --no-cache alpine-sdk

RUN wget -qO-\
    https://github.com/aldostools/webMAN-MOD/archive/${WEBMAN_VERSION}.tar.gz \
    | tar xzf - -C /tmp

WORKDIR /tmp/webMAN-MOD-$WEBMAN_VERSION/_Projects_/ps3netsrv
RUN rm Makefile && mv Makefile.linux Makefile

RUN make BUILD_TYPE=release_static

RUN mv ./ps3netsrv /tmp/ps3netsrv

FROM alpine:${ALPINE_VERSION}

ENV PORT=8080
ENV IP_WHITELIST=192.168.1.*

EXPOSE 8080

COPY --from=build /tmp/ps3netsrv /usr/bin/ps3netsrv

RUN mkdir /games


CMD ps3netsrv /games $PORT $IP_WHITELIST
