FROM digrouz/docker-alp-ddclient
MAINTAINER Andrew Kvalheim <Andrew@Kvalhe.im>

# Simple name resolution command for use in ddclient.conf
RUN apk add --no-cache drill
ADD resolve /usr/local/bin/resolve

# Persistent cache
VOLUME /var/cache/ddclient
