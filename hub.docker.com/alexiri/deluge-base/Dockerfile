FROM alpine:edge

# environment variables
ENV PYTHON_EGG_CACHE="/config/plugins/.python-eggs"

RUN \
  echo "**** install build packages ****" && \
  apk add --no-cache --virtual=build-dependencies \
    g++ \
    gcc \
    libffi-dev \
    openssl-dev \
    py2-pip \
    python2-dev && \
  echo "**** install runtime packages ****" && \
  apk add --no-cache \
    ca-certificates \
    curl \
    libressl2.7-libssl \
    openssl \
    p7zip \
    unrar \
    unzip && \
  apk add --no-cache \
    --repository http://nl.alpinelinux.org/alpine/edge/testing \
    deluge && \
  echo "**** install pip packages ****" && \
  pip install --no-cache-dir -U \
    incremental \
    pip && \
  pip install --no-cache-dir -U \
    crypto \
    mako \
    markupsafe \
    pyopenssl \
    service_identity \
    six \
    twisted \
    zope.interface && \
  echo "**** cleanup ****" && \
    apk del --purge \
    build-dependencies && \
  rm -rf \
    /root/.cache

VOLUME /config /downloads
