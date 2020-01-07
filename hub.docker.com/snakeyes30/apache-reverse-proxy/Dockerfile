FROM httpd:2-alpine
RUN apk add --no-cache curl
ENV DESTINATION_URL=http://localhost:81 \
    PRESERVE_HOST=On \
    SSL_PROXY_ENGINE=On
COPY conf/httpd.conf /usr/local/apache2/conf/httpd.conf
COPY conf/extra/httpd-status.conf /usr/local/apache2/conf/extra/httpd-status.conf
COPY conf/extra/httpd-proxy.conf /usr/local/apache2/conf/extra/httpd-proxy.conf
RUN apachectl
HEALTHCHECK \
    --interval=10s \
    --timeout=5s   \
    --retries=10    \
    CMD curl --fail http://localhost:81/ >/dev/null 2>&1 || exit 1