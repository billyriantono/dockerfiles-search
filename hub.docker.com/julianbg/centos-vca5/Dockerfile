FROM vcatechnology/centos-ci
MAINTAINER VCA Technology <developers@vcatechnology.com>

# Build-time metadata as defined at http://label-schema.org
ARG PROJECT_NAME
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="$PROJECT_NAME" \
      org.label-schema.description="An up-to-date CentOS image that has VCA tool chain packages installed" \
      org.label-schema.url="https://www.centos.org/" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/vcatechnology/docker-centos-toolchain" \
      org.label-schema.vendor="VCA Technology" \
      org.label-schema.version=$VERSION \
      org.label-schema.license=MIT \
      org.label-schema.schema-version="1.0"

# Install useful packages
RUN sudo vca-install-package \
  gcc \
  gcc-c++ \
  make \
  python-pip \
  flex \
  bison \
  zlib-static \
  SDL-static \
  compat-libstdc++-33.i686

# Install python packages
RUN pip install --user \
  backports.functools_lru_cache \
  cpplint
