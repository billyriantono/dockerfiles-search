FROM alpine:latest

LABEL maintainer="Finbarrs Oketunji <oketunjifinbarrs@gmail.com>"

RUN apk update \
    && apk upgrade \
    && apk add --no-cache bash \
    && apk add ca-certificates \
    && rm -rf /var/cache/apk/*

COPY bin/ /usr/local/lib/ssl/
COPY template/ /usr/local/etc/ssl/template/
RUN chmod +x -R /usr/local/lib/ssl/

VOLUME ["/etc/ssl/certs/", "/usr/local/share/ca-certificates/ca/"]
ENTRYPOINT ["/usr/local/lib/ssl/entrypoint.sh"]
