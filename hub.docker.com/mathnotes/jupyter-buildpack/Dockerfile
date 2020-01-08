FROM mathnotes/jupyter:2019-08-21
MAINTAINER Ryan Jensen <ryan.jensen@mathnotes.cc>

USER root
RUN apt-get update && \
  apt-get install -yq --no-install-recommends \
  autoconf \
  automake \
  bzip2 \
  dpkg-dev \
  file \
  g++ \
  gcc \
  imagemagick \
  libbz2-dev \
  libc6-dev \
  libcurl4-openssl-dev \
  libdb-dev \
  libevent-dev \
  libffi-dev \
  libgdbm-dev \
  libgeoip-dev \
  libglib2.0-dev \
  libgmp-dev \
  libjpeg-dev \
  libkrb5-dev \
  liblzma-dev \
  libmagickcore-dev \
  libmagickwand-dev \
  libncurses5-dev \
  libncursesw5-dev \
  libpng-dev \
  libpq-dev \
  libreadline-dev \
  libsqlite3-dev \
  libssl-dev \
  libtool \
  libwebp-dev \
  libxml2-dev \
  libxslt-dev \
  libyaml-dev \
  make \
  patch \
  unzip \
  xz-utils \
  zlib1g-dev \
  wget && \
  rm -rf /var/lib/apt/lists/*

# Runtime Configuration
USER $MN_USER
WORKDIR $MN_HOME

CMD jupyter notebook \
  --no-browser \
  --ip=* \
  --port=8888 \
  --NotebookApp.token='' \
  --NotebookApp.password=''

# Expose Ports
EXPOSE 8888
