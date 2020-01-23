FROM alpine:latest
ARG URL=http://cdn-fastly.deb.debian.org/debian/pool/main/s/systemd/systemd_241-7~deb10u2_amd64.deb
RUN apk add --update curl && rm -rf /var/cache/apk/* 
RUN curl -JkLO $URL
