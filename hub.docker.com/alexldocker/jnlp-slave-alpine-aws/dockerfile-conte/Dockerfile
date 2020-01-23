FROM alpine:3.9
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

# Add Script
COPY docker-entrypoint.sh /usr/bin/

RUN set -xe \
    \
# Install transmission-daemon and shadow (shadow allows us to use 'usermod' and 'groupmod')
    && apk --no-cache add transmission-daemon shadow sudo tini \
    \
# Make a config directory
    && mkdir -p /transmission/config \
    && chmod -R 1777 /transmission \
    \
# Make script executable
    && chmod +x /usr/bin/docker-entrypoint.sh \
    \
# Cleanup
    && rm -rf /tmp/*

# Healthcheck
HEALTHCHECK --interval=60s --timeout=15s \
            CMD netstat -lntp | grep -q '0\.0\.0\.0:9091'

# Default UID/GID
ENV USERID=1000 GROUPID=1000

# Run
ENTRYPOINT ["/sbin/tini", "--", "/usr/bin/docker-entrypoint.sh"]
