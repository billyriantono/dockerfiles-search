# ------------------------------------------------------------------------------
# build stage 1
# ------------------------------------------------------------------------------
FROM hiracchi/alpine-openmpi as openmpi-base

# ------------------------------------------------------------------------------
# build stage 2
# ------------------------------------------------------------------------------
FROM hiracchi/alpine-buildbase as build-base

ARG SCALAPACK_VER=2.0.2

# install dev packages =======================================================--
RUN set -x \
  && apk add --no-cache --virtual .system \
    bash shadow sudo \
  && apk add --no-cache --virtual .dev \
    make cmake musl-dev \
    gcc g++ gfortran \
    clang \
    file patch unzip git curl \
    perl \
  && apk add --no-cache --virtual .linear-algebra-packages \
    openblas openblas-dev

# setup OpenMPI
COPY --from=openmpi-base /opt/openmpi /opt/openmpi
ENV PATH="/opt/openmpi/bin:${PATH}"

# ScaLAPACK ====================================================================
RUN set -x \
  && cd /tmp \
  && curl -O "http://www.netlib.org/scalapack/scalapack-${SCALAPACK_VER}.tgz" \
  && tar zxvf scalapack-${SCALAPACK_VER}.tgz \
  && cd scalapack-${SCALAPACK_VER} \
  && mkdir build \
  && cd build \
  && cmake -DCMAKE_INSTALL_PREFIX=/opt/scalapack .. \
  && make \
  && make install \
  && rm -rf /tmp/scalapack-${SCALAPACK_VER}

# ------------------------------------------------------------------------------
# release stage
# ------------------------------------------------------------------------------
FROM alpine:3.7
MAINTAINER Toshiyuki HIRANO <hiracchi@gmail.com>

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/hiracchi/docker-alpine-scalapack" \
      org.label-schema.version=$VERSION

ENV PATH="${OPENMPI_PATH}/bin:${PATH}"
COPY --from=build-base /opt/scalapack /opt/scalapack
