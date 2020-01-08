FROM debian:stable-slim
LABEL Author="Janic Duplessis <janicduplessis@gmail.com>"
LABEL Description="Th3rdwave base image for CI on linux"

ARG WATCHMAN_VERSION=4.9.0
ARG YARN_VERSION=1.17.3
ARG NODE_VERSION=10.x

# Some apt stuff that needs to be installed first
RUN mkdir -p /usr/share/man/man1 && apt-get update -qq && apt-get install -qq -y --no-install-recommends \
  apt-transport-https \
  apt-utils \
  autoconf \
  automake \
  build-essential \
  ca-certificates \
  curl \
  file \
  git \
  gnupg2 \
  libssl-dev \
  libtool \
  openssh-client \
  pkg-config \
  software-properties-common \
  unzip

# NodeJS
RUN curl -sL "https://deb.nodesource.com/setup_$NODE_VERSION" | bash - \
  && apt-get install -qq -y --no-install-recommends nodejs

# Yarn
RUN curl -fSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
  && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
  && ln -snf /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
  && ln -snf /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
  && rm yarn-v$YARN_VERSION.tar.gz
RUN yarn --version

# Watchman
RUN cd /tmp && curl -LO https://github.com/facebook/watchman/archive/v${WATCHMAN_VERSION}.tar.gz \
  && tar xzf v${WATCHMAN_VERSION}.tar.gz \
  && rm v${WATCHMAN_VERSION}.tar.gz \
  && cd watchman-${WATCHMAN_VERSION} \
  && ./autogen.sh \
  && ./configure --without-python --without-pcre --enable-lenient \
  && make \
  && make install \
  && rm -rf watchman-${WATCHMAN_VERSION}
