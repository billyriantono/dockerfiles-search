FROM alpine:latest

# Install packages
RUN apk update && \
    apk add --no-cache \
    lighttpd \
    openssl \
    curl && \
    rm -rf /var/cache/apk/*

# Copy lighttpd config files. At this point it is all default except
# including a custom ssl.conf in lighttpd.conf.
COPY config/lighttpd/*.conf /etc/lighttpd/

# Copy an example index.html to the default webroot to allow
# for demo/testing without needing mounts during `docker run`
COPY htdocs/index.html /var/www/localhost/htdocs/

# Check every minute if lighttpd responds within 1 second and update
# container health status accordingly.
HEALTHCHECK --interval=1m --timeout=1s \
  CMD curl -f http://localhost/ || exit 1

# Expose http(s) ports
EXPOSE 1080

# Make configuration path and webroot a volume
VOLUME /etc/lighttpd/
VOLUME /var/www/
VOLUME /var/log/lighttpd

ENTRYPOINT ["/usr/sbin/lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
