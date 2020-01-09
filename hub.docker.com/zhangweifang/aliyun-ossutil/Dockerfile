FROM alpine as certs
RUN apk update && apk add ca-certificates

FROM busybox:glibc
COPY --from=certs /etc/ssl/certs /etc/ssl/certs

ENV OSSUTIL_VER 1.6.9
RUN mkdir -p /usr/local/bin \
    && wget http://gosspublic.alicdn.com/ossutil/${OSSUTIL_VER}/ossutil64 -O /usr/local/bin/ossutil \
    && chmod 755 /usr/local/bin/ossutil
VOLUME ["/root"]

