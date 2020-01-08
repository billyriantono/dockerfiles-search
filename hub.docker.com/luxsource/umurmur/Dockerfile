FROM alpine:edge

RUN apk update

# Debug
    # RUN apk add bash

# Install umurmur
    RUN apk add umurmur

# Clean
    RUN rm -rf /var/cache/apk/*

# Defaults
    EXPOSE 64738
    STOPSIGNAL SIGTERM
    ENTRYPOINT ["/usr/bin/umurmurd", "-d", "-c", "/etc/umurmur/umurmurd.conf"]

