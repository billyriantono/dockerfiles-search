FROM develar/java:8u45

RUN printf "http://dl-cdn.alpinelinux.org/alpine/v3.3/main\nhttp://dl-cdn.alpinelinux.org/alpine/v3.3/community\n" > /etc/apk/repositories

RUN apk update && apk add bash haproxy supervisor && apk upgrade \
    && rm -rf /var/cache/apk/*
ENTRYPOINT []

