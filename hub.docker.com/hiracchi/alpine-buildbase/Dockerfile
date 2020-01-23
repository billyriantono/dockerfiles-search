FROM alpine:3.7

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/hiracchi/docker-alpine-buildbase" \
      org.label-schema.version=$VERSION

RUN set -x \
  && apk add --no-cache \
    tzdata \
  && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
  && apk add --no-cache --virtual .system \
    bash shadow sudo \
  && apk add --no-cache --virtual .editor \
    emacs vim \
  && apk add --no-cache --virtual .python \
    python3 \
  && apk add --no-cache --virtual .perl \
    perl \
  && apk add --no-cache --virtual .dev \
    make cmake musl-dev \
    gcc g++ gfortran \
    clang \
    file patch unzip git curl \
  && apk add --no-cache --virtual .dev-python \
    python3-dev \
    freetype-dev libpng-dev libjpeg-turbo-dev \
    libxml2-dev libxslt-dev \
  && apk add --no-cache --virtual .libs \
    freetype libpng libjpeg-turbo \
    libxml2 libxslt \
  && apk add --no-cache --virtual .linear-algebra-packages \
    openblas openblas-dev \
  && apk add --no-cache --virtual .dev-opencl \
    opencl-headers opencl-icd-loader
