FROM openjdk:jre-alpine

LABEL \
    maintainer="Morgan AUCHEDE <morgan.auchede@gmail.com>"

RUN set -e -u -x \
\
    # Install packages
\
    && apk add --no-cache --no-progress --virtual BUILD_DEPS bash curl \
\
    # Install dumb-entrypoint
\
    && curl --location "https://gitlab.com/timonier/dumb-entrypoint/raw/master/src/dumb-entrypoint/installer" | bash -s -- install \
    && curl --location "https://gitlab.com/timonier/dumb-entrypoint/raw/master/src/gosu/installer" | bash -s -- install \
\
    # Install wiremock
\
    && export $(curl --location "https://gitlab.com/timonier/version-lister/raw/generated/tomakehurst/wiremock/latest" | xargs) \
    && mkdir -p /opt/wiremock \
    && curl --location --output /opt/wiremock/wiremock.jar "${WIREMOCK_RELEASE}" \
\
    # Clean
\
    && apk del --no-progress BUILD_DEPS

COPY rootfs/ /

ENTRYPOINT [ "dumb-entrypoint" ]
