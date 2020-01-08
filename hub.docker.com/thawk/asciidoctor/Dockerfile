FROM asciidoctor/docker-asciidoctor:latest

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/thawk/asciidoctor.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="1.0.0-rc1"

RUN apk add --no-cache \
    cabal \
&&  apk add --no-cache --virtual .makedepends \
    git \
    ghc \
    build-base \
    libxml2-dev \
    python2-dev \
    py2-pip \
    ruby-dev \
    zlib-dev \
&&  cabal update \
&&  cabal install graphviz parsec text \
&&  cd /tmp/ && git clone git://github.com/BurntSushi/erd \
&&  cd erd \
&&  cabal configure \
&&  cabal build \
&&  mv dist/build/erd/erd /usr/bin/ && cd ../ && rm -rf erd \
&&  apk del -r --no-cache .makedepends
