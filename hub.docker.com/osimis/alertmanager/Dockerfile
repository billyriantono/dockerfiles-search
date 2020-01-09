ARG ALPINE_VERSION

FROM alpine:$ALPINE_VERSION as setup
ARG VER
ARG PKG=alertmanager-$VER.linux-amd64
ARG FGP
COPY setup.sh /usr/local/bin/
RUN setup.sh "$VER" "$PKG" "$FGP"

FROM alpine:$ALPINE_VERSION
ENTRYPOINT ["entrypoint.sh"]
RUN apk add --no-cache bash=4.4.12-r2 ca-certificates=20171114-r0
COPY entrypoint.sh /usr/local/bin/
COPY --from=setup /alertmanager /usr/local/bin/
