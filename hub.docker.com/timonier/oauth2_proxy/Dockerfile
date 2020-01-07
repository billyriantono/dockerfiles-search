FROM alpine:latest

LABEL \
    maintainer="Morgan Auchede <morgan.auchede@gmail.com>"

RUN set -e -u -x \
\
    # Install packages
\
    && apk add --no-cache --no-progress --virtual BUILD_DEPS curl \
    && apk add --no-cache --no-progress ca-certificates \
\
    # Install dumb-entrypoint
\
    && curl --location "https://github.com/timonier/dumb-entrypoint/raw/master/src/dumb-entrypoint/installer" | sh -s -- install \
    && curl --location "https://github.com/timonier/dumb-entrypoint/raw/master/src/gosu/installer" | sh -s -- install \
\
    # Install oauth2_proxy
\
    && export $(curl --location "https://github.com/timonier/version-lister/raw/generated/bitly/oauth2_proxy/latest" | xargs) \
    && curl --location "${OAUTH2_PROXY_RELEASE}" | tar --directory /tmp --extract --gzip \
    && mv /tmp/oauth2_proxy-"${OAUTH2_PROXY_VERSION}".linux-amd64.go"${OAUTH2_PROXY_GO_VERSION}"/oauth2_proxy /usr/local/bin/oauth2_proxy \
\
    # Clean
\
    && apk del --no-progress BUILD_DEPS \
    && rm -f -r /tmp/*

ENTRYPOINT [ "dumb-entrypoint" ]
