FROM alpine:3.7

MAINTAINER Alex Shvedov <alexeii.shvedov@gmailc.om>

ARG ALPINE_REPO=http://dl-cdn.alpinelinux.org

ENV TIMEZONE Asia/Novosibirsk
ENV GLIBC_VERSION=2.26-r0

# glibc setup
RUN set -ex && apk update && apk upgrade && \

    # Make info file about this build
    mkdir -p /etc/BUILDS/ && \
    printf "Build of nimmis/alpine-glibc:3.5, date: %s\n"  `date -u +"%Y-%m-%dT%H:%M:%SZ"` > /etc/BUILDS/alpine-glibc && \

    # add curl for download
    apk add --no-cache curl && \

    # download packages for glibc, see https://github.com/sgerrand/alpine-pkg-glibc for more info
    curl -L -o glibc-${GLIBC_VERSION}.apk \
      "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk" && \
    curl -L -o glibc-bin-${GLIBC_VERSION}.apk \
      "https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-bin-${GLIBC_VERSION}.apk" && \

    # install them
    apk add --no-cache --allow-untrusted glibc-${GLIBC_VERSION}.apk glibc-bin-${GLIBC_VERSION}.apk && \

    # remove curl
    apk del curl && \

    # remove cache and downloaded files
    rm -fr glibc-${GLIBC_VERSION}.apk glibc-bin-${GLIBC_VERSION}.apk /var/cache/apk/*

# sync setup with deps
RUN set -ex && ver=$(cat /etc/alpine-release | awk -F '.' '{printf "%s.%s", $1, $2;}') \
    && repos=/etc/apk/repositories \
    && mv -f ${repos} ${repos}_bk \
    && echo "${ALPINE_REPO}/alpine/v${ver}/main" > ${repos} \
    && echo "${ALPINE_REPO}/alpine/v${ver}/community" >> ${repos} \
    \
    && apk --no-cache add tzdata bash \
    && ln -sf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
    && echo "${TIMEZONE}" > /etc/timezone \
    \
    && apk --no-cache add wget ca-certificates su-exec \
    && cd /tmp \
    && wget https://download-cdn.resilio.com/stable/linux-x64/resilio-sync_x64.tar.gz \
    && tar xzf resilio-sync_x64.tar.gz \
    && mv rslsync /usr/local/bin

COPY sync.conf.default /etc/

EXPOSE 8888
EXPOSE 55555

VOLUME ["/sync", "/storage"]

ENTRYPOINT ["run_sync.sh"]
CMD ["--config", "/sync/sync.conf"]

COPY run_sync.sh /usr/bin/