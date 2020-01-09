FROM alpine:latest
LABEL maintainer="Meraj Sahebdar <itsdrewstiles@gmail.com>" \
    com.treillage.name="base" \
    com.treillage.vendor="treillage" \
    com.treillage.vcs-url="https://github.com/treillage/images" \
    com.treillage.version="1.0.0" \
    com.treillage.license="MIT"

ENV TERM="xterm" \
    LANG="C.UTF-8" \
    LC_ALL="C.UTF-8"
ENV SVDIR="/opt/service"

COPY add-on/ /opt/

RUN set -x \
    # Upgrade Alpine to the latest
    && apk upgrade --no-cache --force \
    # Install base utilities
    && apk add --no-cache --upgrade \
        bash \
        ca-certificates \
        curl \
        grep \
        openssl \
        runit \
        sed \
        shadow \
        su-exec \
        tzdata \
    && update-ca-certificates \
    # Install extra utilities
    && curl -L "https://github.com/treillage/images-utilities/archive/master.tar.gz" | tar -xzvC / --strip-components 2 images-utilities-master/baselayout \
    && find /usr/local/bin -type f -exec chmod +x {} \; \
    && curl -Lo /usr/local/bin/envsubst "https://raw.githubusercontent.com/treillage/envsubst/master/envsubst" \
    && chmod +x /usr/local/bin/envsubst \
    # Cleanup image
    && image-build \
    && image-clean

ENTRYPOINT ["/usr/local/bin/image-entry"]
CMD ["runsvdir"]
