FROM debian:stable-slim

LABEL \
    maintainer="Morgan AUCHEDE <morgan.auchede@gmail.com>"

ENV \
    S6_BEHAVIOUR_IF_STAGE2_FAILS=2 \
    S6_KEEP_ENV=1 \
    S6_READ_ONLY_ROOT=1

RUN set -e -u -x \
\
    # Prepare system
\
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
\
    # Install packages
\
    && BUILD_DEPS="build-essential curl gnutls-dev libcurl4-gnutls-dev python-dev python-pip" \
    && apt-get install --no-install-recommends --yes ${BUILD_DEPS} \
    && apt-get install --no-install-recommends --yes ca-certificates locales python-opencv python-setuptools \
\
    # Install dockerize
\
    && curl --location "https://gitlab.com/timonier/dumb-entrypoint/raw/master/src/dockerize/installer" | bash -s -- install \
\
    # Install s6-overlay
\
    && curl --location "https://gitlab.com/timonier/dumb-entrypoint/raw/master/src/s6-overlay/installer" | bash -s -- install \
\
    # Install thumbor
\
    && pip install thumbor \
\
    # Clean
\
    && apt-get remove --purge --yes ${BUILD_DEPS} \
    && apt-get autoremove --purge --yes \
    && rm -f -r /tmp/* /var/lib/apt/lists/*

COPY rootfs/ /

ENTRYPOINT [ "/init" ]
