FROM akilli/base

LABEL maintainer="Ayhan Akilli"

RUN apk add --no-cache redis && \
    rm -rf /var/lib/redis && \
    chown -R app:app /run/redis && \
    app-user && \
    app-chown

COPY s6/ /s6/redis/
