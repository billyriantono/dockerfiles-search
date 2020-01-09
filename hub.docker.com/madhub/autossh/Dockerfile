FROM alpine:3.9
MAINTAINER Franz Mathauser <franz.mathauser@gmail.com>

RUN apk update && \
    apk add autossh && \
    rm -r /var/cache/

EXPOSE 80

ENTRYPOINT [ "autossh"]
