FROM alpine

LABEL manitainer="Apontador Team"

COPY download-files.sh /usr/local/bin/
COPY docker-entrypoint.sh /usr/local/bin/

RUN chmod +x /usr/local/bin/download-files.sh \
    && ln -s /usr/local/bin/download-files.sh /download-files.sh \
    && chmod +x /usr/local/bin/docker-entrypoint.sh \
    && ln -s /usr/local/bin/docker-entrypoint.sh /docker-entrypoint.sh
