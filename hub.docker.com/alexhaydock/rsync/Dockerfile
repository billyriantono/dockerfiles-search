FROM alpine:3.9
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

COPY docker-entrypoint.sh /usr/bin/

RUN apk --no-cache add rsync openssh-client bash shadow sudo tini \
    \
# Add 'user' user and group with IDs of 1000
    && addgroup -S rsync \
    && adduser -D -S -s /sbin/nologin -G rsync rsync \
    && usermod -u 1000 -o rsync \
    && groupmod -g 1000 -o rsync \
    \
# Make script executable
    && chmod +x /usr/bin/docker-entrypoint.sh

# Default
ENV USERID=1000 GROUPID=1000

ENTRYPOINT [ "/sbin/tini", "--", "/usr/bin/docker-entrypoint.sh" ]
