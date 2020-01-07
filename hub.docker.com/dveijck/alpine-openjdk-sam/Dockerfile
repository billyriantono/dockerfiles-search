FROM dveijck/alpine-awscli:3.8_1.16.60

RUN apk --no-cache update && \
    apk --no-cache add ca-certificates wget && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk && \
    apk add glibc-2.28-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-bin-2.28-r0.apk && \
    apk add glibc-bin-2.28-r0.apk && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-i18n-2.28-r0.apk && \
    apk add glibc-i18n-2.28-r0.apk && \
    apk --no-cache add gcc && \
    apk --no-cache add musl-dev && \
    apk --no-cache add openjdk8 && \
    apk --no-cache add python3-dev && \
    pip3 install aws-sam-cli==v0.7.0 && \
    rm -rf /var/cache/apk/* && \
    rm glibc-*.apk
