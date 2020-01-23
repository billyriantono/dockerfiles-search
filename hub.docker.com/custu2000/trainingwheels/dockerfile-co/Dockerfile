FROM anigeo/awscli

RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.4/community" >> /etc/apk/repositories && \
    apk update && \
    apk add docker==1.11.2-r1 && \
    rm -rf /var/cache/apk/*
