#-----------------------------------
# Type:    Base image
# For:     Node applications
# Image:   kapott/node
# Size:    ~22 MB
#-----------------------------------

FROM alpine
MAINTAINER Tom Meurs <tom@byteherder.com>
RUN apk --update add nodejs \
    && mkdir -p /app \
    && rm -rf /var/cache/apk/*

VOLUME ["/app"]

ENTRYPOINT ["node", "/app"]