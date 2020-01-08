FROM buildkite/agent:3
MAINTAINER Jason Cox <jason.cox@panoply.fm>

ADD VERSION .

# ruby
# -----------
RUN mkdir -p /usr/local/etc \
  && { \
    echo 'install: --no-document'; \
    echo 'update: --no-document'; \
  } >> /usr/local/etc/gemrc

ENV RUBY_VERSION 2.3.3
ENV RUBYGEMS_VERSION 2.6.10

RUN set -ex \
  && apk add --update --no-cache \
    autoconf \
    bash \
    bison \
    bzip2 \
    bzip2-dev \
    ca-certificates \
    coreutils \
    curl \
    gcc \
    git \
    gdbm-dev \
    glib-dev \
    libc-dev \
    libffi-dev \
    libxml2-dev \
    libxslt-dev \
    linux-headers \
    make \
    ncurses-dev \
    postgresql-dev \
    procps \
    readline-dev \
    yaml-dev \
    zlib-dev \
    ruby \
    ruby-dev

ENV PATH /usr/local/rbenv/shims:/usr/local/rbenv/bin:$PATH
ENV RBENV_ROOT /usr/local/rbenv
ENV CONFIGURE_OPTS="ac_cv_func_isnan=yes ac_cv_func_isinf=yes --disable-install-doc"

RUN git clone --depth 1 git://github.com/sstephenson/rbenv.git ${RBENV_ROOT} \
&&  git clone --depth 1 https://github.com/sstephenson/ruby-build.git ${RBENV_ROOT}/plugins/ruby-build \
&&  git clone --depth 1 git://github.com/jf/rbenv-gemset.git ${RBENV_ROOT}/plugins/rbenv-gemset \
&& ${RBENV_ROOT}/plugins/ruby-build/install.sh

RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh

RUN rbenv install $RUBY_VERSION && \
  rbenv global $RUBY_VERSION

RUN gem install bundler

# faster nokogiri installs
RUN bundle config build.nokogiri --use-system-libraries

# Install globally, don't create ".bundle" in all our apps
ENV GEM_HOME /usr/local/bundle
ENV BUNDLE_PATH="$GEM_HOME" \
  BUNDLE_BIN="$GEM_HOME/bin" \
  BUNDLE_SILENCE_ROOT_WARNING=1 \
  BUNDLE_APP_CONFIG="$GEM_HOME"
ENV PATH $BUNDLE_BIN:$PATH
RUN mkdir -p "$GEM_HOME" "$BUNDLE_BIN" \
  && chmod 777 "$GEM_HOME" "$BUNDLE_BIN"
# -----------

# node
# ----------
RUN set -ex \
  && apk add --no-cache --virtual .build-deps \
    binutils-gold \
    curl \
    g++ \
    gcc \
    gnupg \
    libgcc \
    linux-headers \
    make \
    python \
    libstdc++ \
    ncurses \
    ca-certificates \
    openssl \
    coreutils \
    python2 \
    grep \
    util-linux \
    binutils \
    findutils

# nvm node version manager
RUN wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | /bin/bash
ENV NVM_DIR /root/.nvm
RUN [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
  nvm install -s 9.11 && nvm use 9.11
RUN [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
  npm install -g yarn
RUN echo "source $NVM_DIR/nvm.sh" >> /etc/profile.d/nvm.sh
RUN echo "source $NVM_DIR/nvm.sh" >> $HOME/.bashrc
# ----------

# golang
# ----------
ENV GOLANG_VERSION 1.9.4
RUN set -eux; \
	apk add --no-cache --virtual .build-deps \
		bash \
		gcc \
		musl-dev \
		openssl \
		go

ENV GOROOT_BOOTSTRAP=/usr/lib/go GOOS=linux GOARCH=amd64 GOHOSTOS=linux GOHOSTARCH=amd64 GO386=387
ENV GOPATH $HOME/go
ENV PATH $GOPATH/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"

RUN ["/bin/bash", "-c", "bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)"]
RUN ["/bin/bash", "-c", "source /root/.gvm/scripts/gvm && gvm install go1.10 && gvm use go1.10"]
RUN echo "source /root/.gvm/scripts/gvm" >> /etc/profile.d/gvm.sh
RUN echo "source /root/.gvm/scripts/gvm" >> $HOME/.bashrc

# install dep
RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
# ----------

# set up phantomjs
RUN apk update && apk add --no-cache fontconfig && \
  wget -qO- "https://github.com/dustinblackman/phantomized/releases/download/2.1.1a/dockerized-phantomjs.tar.gz" | tar xz -C / && \
  [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
  npm config set user 0 && \
  npm install -g phantomjs-prebuilt

RUN apk add --update -X http://dl-cdn.alpinelinux.org/alpine/edge/testing chromaprint-dev
RUN apk add --no-cache tini sudo chromaprint

# allow ssh config
RUN curl -fL "https://raw.githubusercontent.com/buildkite/docker-ssh-env-config/d06f20bdc7457a647bfe3724d94525f83c863091/ssh-env-config.sh" -o /usr/local/bin/ssh-env-config.sh \
    && chmod +x /usr/local/bin/ssh-env-config.sh

ADD init.sh /usr/local/bin/init.sh
RUN chmod +x /usr/local/bin/init.sh
ENTRYPOINT ["/sbin/tini", "--", "init.sh"]
CMD ["start"]
