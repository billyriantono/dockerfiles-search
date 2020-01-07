FROM wordpress

COPY docker-entrypoint.patch /tmp

RUN cd /usr/local/bin; patch < /tmp/docker-entrypoint.patch

