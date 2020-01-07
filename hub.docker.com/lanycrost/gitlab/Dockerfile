FROM lanycrost/alpine:3.8

LABEL maintainer="Khachatur Ashotyan (lanycrost)"
LABEL version="0.1"
LABEL description="GitLab CE w/S6 Overlay based on Alpine."

ENV RUBY_MAJOR=2.4
ENV RUBY_VERSION=2.4.4
ENV RUBY_DOWNLOAD_SHA256=1d0034071d675193ca769f64c91827e5f54cb3a7962316a41d5217c7bc6949f0
ENV RUBYGEMS_VERSION=2.7.7
ENV BUNDLER_VERSION=1.16.2

ENV GITLAB_VERSION="11.2.0"
ENV GITLAB_SHELL_VERSION="8.1.1"
ENV GITLAB_WORKHORSE_VERSION="5.1.0"
ENV GITLAB_PAGES_VERSION="1.0.0"
ENV GITALY_SERVER_VERSION="0.117.2"
ENV GITLAB_USER="root"
ENV GITLAB_HOME="/home/git"
ENV RAILS_ENV="production"
ENV NODE_ENV="production"

ENV GITLAB_INSTALL_DIR="${GITLAB_HOME}/gitlab"
ENV GITLAB_SHELL_INSTALL_DIR="${GITLAB_HOME}/gitlab-shell"
ENV GITLAB_WORKHORSE_INSTALL_DIR="${GITLAB_HOME}/gitlab-workhorse"
ENV GITLAB_PAGES_INSTALL_DIR="${GITLAB_HOME}/gitlab-pages"
ENV GITLAB_GITALY_INSTALL_DIR="${GITLAB_HOME}/gitaly"
ENV GITLAB_DATA_DIR="${GITLAB_HOME}/data"
ENV GITLAB_BUILD_DIR="/usr/src"
ENV GITLAB_RUNTIME_DIR="${GITLAB_HOME}/runtime"
ENV GITLAB_LOG_DIR="/var/log"
ENV MODE="START"

RUN set -ex && \
    mkdir -p /usr/local/etc \ && \
	{ \
		echo 'install: --no-document'; \
		echo 'update: --no-document'; \
	} >> /usr/local/etc/gemrc

# some of ruby's build scripts are written in ruby
#   we purge system ruby later to make sure our final image uses what we just built
# readline-dev vs libedit-dev: https://bugs.ruby-lang.org/issues/11869 and https://github.com/docker-library/ruby/issues/75
RUN set -ex \
	\
	&& apk add --no-cache --virtual .ruby-builddeps \
		autoconf \
		bison \
		bzip2 \
		bzip2-dev \
		ca-certificates \
		coreutils \
		dpkg-dev dpkg \
		gcc \
		gdbm-dev \
		glib-dev \
		libc-dev \
		libffi-dev \
		openssl \
		openssl-dev \
		libxml2-dev \
		libxslt-dev \
		linux-headers \
		make \
		ncurses-dev \
		procps \
		readline-dev \
		ruby \
		tar \
		xz \
		yaml-dev \
		zlib-dev \
	\
	&& wget -O ruby.tar.xz "https://cache.ruby-lang.org/pub/ruby/${RUBY_MAJOR%-rc}/ruby-$RUBY_VERSION.tar.xz" \
	&& echo "$RUBY_DOWNLOAD_SHA256 *ruby.tar.xz" | sha256sum -c - \
	\
	&& mkdir -p /usr/src/ruby \
	&& tar -xJf ruby.tar.xz -C /usr/src/ruby --strip-components=1 \
	&& rm ruby.tar.xz \
	\
	&& cd /usr/src/ruby \
	\
# hack in "ENABLE_PATH_CHECK" disabling to suppress:
#   warning: Insecure world writable dir
	&& { \
		echo '#define ENABLE_PATH_CHECK 0'; \
		echo; \
		cat file.c; \
	} > file.c.new \
	&& mv file.c.new file.c \
	\
	&& autoconf \
	&& gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" \
# the configure script does not detect isnan/isinf as macros
	&& export ac_cv_func_isnan=yes ac_cv_func_isinf=yes \
	&& ./configure \
		--build="$gnuArch" \
		--disable-install-doc \
		--enable-shared \
	&& make -j "$(nproc)" \
	&& make install \
	\
	&& runDeps="$( \
		scanelf --needed --nobanner --format '%n#p' --recursive /usr/local \
			| tr ',' '\n' \
			| sort -u \
			| awk 'system("[ -e /usr/local/lib/" $1 " ]") == 0 { next } { print "so:" $1 }' \
	)" \
	&& apk add --virtual .ruby-rundeps $runDeps \
		bzip2 \
		ca-certificates \
		libffi-dev \
		procps \
		yaml-dev \
		zlib-dev \
	&& apk del .ruby-builddeps \
	&& cd / \
	&& rm -r /usr/src/ruby \
	\
	&& gem update --system "$RUBYGEMS_VERSION" \
	&& gem install bundler --version "$BUNDLER_VERSION" --force \
	&& rm -r /root/.gem/

# install things globally, for great justice
# and don't create ".bundle" in all our apps
ENV GEM_HOME /usr/local/bundle
ENV BUNDLE_PATH="$GEM_HOME"
ENV BUNDLE_SILENCE_ROOT_WARNING=1
ENV BUNDLE_APP_CONFIG="$GEM_HOME"

# path recommendation: https://github.com/bundler/bundler/pull/6469#issuecomment-383235438
ENV PATH $GEM_HOME/bin:$BUNDLE_PATH/gems/bin:$PATH

# adjust permissions of a few directories for running "gem install" as an arbitrary user
RUN mkdir -p "$GEM_HOME" && chmod 777 "$GEM_HOME"

# Add User
RUN addgroup -g 1000 -S ${GITLAB_USER} && \
	adduser -u 1000 -D -S -s /bin/bash -G ${GITLAB_USER} ${GITLAB_USER} && \
	sed -i '/^git/s/!/*/' /etc/shadow && \
	echo "PS1='\w\$ '" >> ${GITHOME_HOME}/.bashrc && \
  echo "PATH=/usr/local/sbin:/usr/local/bin:\$PATH" >> ${GITLAB_HOME}/.profile

# Install Dependencies
RUN apk add --update --no-cache -t .gitlab-rundeps \
  git \
  grep \
  icu-libs \
  krb5-libs \
  libc6-compat \
  libre2 \
  openssl \
  make \
  mariadb-client \
  nginx \
  openssh \
  postgresql-client \
  python2 \
  rsync \
  shadow \
  su-exec \
  sudo \
  zip

# Install GitLab build dependencies
RUN apk del openssl-dev libressl-dev && \
  apk add --update --no-cache -t .gitlab-build-deps \
    autoconf \
    build-base \
    cmake \
    coreutils \
    g++ \
    gdbm-dev \
    go \
    icu-dev \
    krb5-dev \
    libassuan-dev \
    libffi-dev \
    libre2-dev \
    libressl-dev \
    libgcrypt-dev \
    libxml2-dev \
    libxslt-dev \
    linux-headers \
    mariadb-dev \
    ncurses-dev \
    nodejs \
    patch \
    postgresql-dev \
    readline-dev \
    sqlite-dev \
    yaml-dev \
    yarn \
    zlib-dev && \
    rm -rf /etc/nginx/conf.d/default.conf

# Temporary install package to get specific bins
RUN apk add --update redis postgresql gettext && \
  cp /usr/bin/redis-cli /tmp && \
  cp /usr/bin/pg_* /tmp && \
  apk del --purge redis postgresql && \
  mv /tmp/redis-cli /usr/bin/ && \
  mv /tmp/pg_* /usr/bin/

# Download and install gitlab.
RUN GITLAB_CLONE_URL=https://gitlab.com/gitlab-org/gitlab-ce.git && \
  mkdir -p ${GITLAB_INSTALL_DIR} && \
  git clone -q -b v${GITLAB_VERSION} --depth 1 ${GITLAB_CLONE_URL} ${GITLAB_INSTALL_DIR} && \
  chown -R ${GITLAB_USER}:${GITLAB_USER} ${GITLAB_INSTALL_DIR} && \
  su-exec git sed -i "/headers\['Strict-Transport-Security'\]/d" ${GITLAB_INSTALL_DIR}/app/controllers/application_controller.rb && \
  cd ${GITLAB_INSTALL_DIR} && \
  chown -R ${GITLAB_USER}:${GITLAB_USER} /usr/local/lib/ruby/gems/2.4.0/ && \
  chown -R ${GITLAB_USER}:${GITLAB_USER} /usr/local/bundle/

WORKDIR ${GITLAB_INSTALL_DIR}

# Install gems (build from source).
RUN export BUNDLE_FORCE_RUBY_PLATFORM=1 && \
  su-exec git bundle install -j$(nproc) --deployment --verbose --without development test aws kerberos

# Make sure everything in ${GITLAB_HOME} is owned by ${GITLAB_USER} user
RUN chown -R ${GITLAB_USER}: ${GITLAB_HOME}

# gitlab.yml and database.yml are required for `assets:precompile`
RUN su-exec git cp ${GITLAB_INSTALL_DIR}/config/resque.yml.example ${GITLAB_INSTALL_DIR}/config/resque.yml && \
  su-exec git cp ${GITLAB_INSTALL_DIR}/config/gitlab.yml.example ${GITLAB_INSTALL_DIR}/config/gitlab.yml && \
  su-exec git cp ${GITLAB_INSTALL_DIR}/config/database.yml.mysql ${GITLAB_INSTALL_DIR}/config/database.yml

# Compile assets
RUN su-exec git yarn install --production --pure-lockfile && \
  su-exec git yarn add ajv@^4.0.0 && \
  su-exec git bundle exec rake gitlab:assets:compile USE_DB=false SKIP_STORAGE_VALIDATION=true

# PO files
RUN su-exec git bundle exec rake gettext:pack && \
  su-exec git bundle exec rake gettext:po_to_json

# Download and Install Gitlab-Shell
RUN GITLAB_SHELL_URL=https://gitlab.com/gitlab-org/gitlab-shell/repository/archive.tar.gz && \
  GITLAB_SHELL_VERSION=${GITLAB_SHELL_VERSION:-$(cat ${GITLAB_INSTALL_DIR}/GITLAB_SHELL_VERSION)} && \
  echo "Downloading gitlab-shell v.${GITLAB_SHELL_VERSION}..." && \
  mkdir -p ${GITLAB_SHELL_INSTALL_DIR} && \
  curl -sSL ${GITLAB_SHELL_URL}?ref=v${GITLAB_SHELL_VERSION} | tar xfvz - --strip 1 -C ${GITLAB_SHELL_INSTALL_DIR} && \
  chown -R ${GITLAB_USER}: ${GITLAB_SHELL_INSTALL_DIR} && \
  \
  cd ${GITLAB_SHELL_INSTALL_DIR} && \
  su-exec git cp -a ${GITLAB_SHELL_INSTALL_DIR}/config.yml.example ${GITLAB_SHELL_INSTALL_DIR}/config.yml && \
  su-exec git ./bin/compile && \
  su-exec git ./bin/install && \
  \
  su-exec git rm -rf ${GITLAB_HOME}/repositories

# Download And Install Gitlab Workhorse
RUN GITLAB_WORKHORSE_URL=https://gitlab.com/gitlab-org/gitlab-workhorse.git && \
  GITLAB_WORKHORSE_VERSION=${GITLAB_WORKHOUSE_VERSION:-$(cat ${GITLAB_INSTALL_DIR}/GITLAB_WORKHORSE_VERSION)} && \
  echo "Cloning gitlab-workhorse v.${GITLAB_WORKHORSE_VERSION}..." && \
  su-exec git git clone -q -b v${GITLAB_WORKHORSE_VERSION} --depth 1 ${GITLAB_WORKHORSE_URL} ${GITLAB_WORKHORSE_INSTALL_DIR} && \
  chown -R ${GITLAB_USER}: ${GITLAB_WORKHORSE_INSTALL_DIR} && \
  cd ${GITLAB_WORKHORSE_INSTALL_DIR} && \
  make install

# Download and Install Gitlab Pages
RUN GITLAB_PAGES_URL=https://gitlab.com/gitlab-org/gitlab-pages.git && \
  GITLAB_PAGES_VERSION=${GITLAB_PAGES_VERSION:-$(cat ${GITLAB_INSTALL_DIR}/GITLAB_PAGES_VERSION)} && \
  echo "Downloading gitlab-pages v.${GITLAB_PAGES_VERSION}..." && \
  su-exec git git clone -q -b v${GITLAB_PAGES_VERSION} --depth 1 ${GITLAB_PAGES_URL} ${GITLAB_PAGES_INSTALL_DIR} && \
  chown -R ${GITLAB_USER}: ${GITLAB_PAGES_INSTALL_DIR} && \
  cd ${GITLAB_PAGES_INSTALL_DIR} && \
  make && \
  cp -f gitlab-pages /usr/local/bin/

# Download and Install Gitaly
RUN GITLAB_GITALY_URL=https://gitlab.com/gitlab-org/gitaly.git && \
  echo "Downloading gitaly v.${GITALY_SERVER_VERSION}..." && \
  su-exec git git clone -q -b v${GITALY_SERVER_VERSION} --depth 1 ${GITLAB_GITALY_URL} ${GITLAB_GITALY_INSTALL_DIR} && \
  chown -R ${GITLAB_USER}: ${GITLAB_GITALY_INSTALL_DIR} && \
  su-exec git cp ${GITLAB_GITALY_INSTALL_DIR}/config.toml.example ${GITLAB_GITALY_INSTALL_DIR}/config.toml && \
  cd ${GITLAB_GITALY_INSTALL_DIR} && \
  export BUNDLE_FORCE_RUBY_PLATFORM=1 && \
  make install && \
  make clean

# Filesystem Cleanup and Setup
# revert `rake gitlab:setup` changes from gitlabhq/gitlabhq@a54af831bae023770bf9b2633cc45ec0d5f5a66a
RUN su-exec git sed -i 's/db:reset/db:setup/' ${GITLAB_INSTALL_DIR}/lib/tasks/gitlab/setup.rake && \
  \
  ### remove auto generated ${GITLAB_DATA_DIR}/config/secrets.yml
  rm -rf ${GITLAB_DATA_DIR}/config/secrets.yml && \
  \
  ### remove gitlab shell and workhorse secrets
  rm -f ${GITLAB_INSTALL_DIR}/.gitlab_shell_secret ${GITLAB_INSTALL_DIR}/.gitlab_workhorse_secret && \
  \
  su-exec git mkdir -p ${GITLAB_INSTALL_DIR}/tmp/pids/ ${GITLAB_INSTALL_DIR}/tmp/sockets/ && \
  chmod -R u+rwX ${GITLAB_INSTALL_DIR}/tmp && \
  \
  ### symlink ${GITLAB_HOME}/.ssh -> ${GITLAB_LOG_DIR}/gitlab
  rm -rf ${GITLAB_HOME}/.ssh && \
  su-exec git ln -sf ${GITLAB_DATA_DIR}/.ssh ${GITLAB_HOME}/.ssh && \
  \
  ### symlink ${GITLAB_INSTALL_DIR}/log -> ${GITLAB_LOG_DIR}/gitlab
  rm -rf ${GITLAB_INSTALL_DIR}/log && \
  ln -sf ${GITLAB_LOG_DIR}/gitlab ${GITLAB_INSTALL_DIR}/log && \
  \
  ### symlink ${GITLAB_INSTALL_DIR}/public/uploads -> ${GITLAB_DATA_DIR}/uploads
  rm -rf ${GITLAB_INSTALL_DIR}/public/uploads && \
  su-exec git ln -sf ${GITLAB_DATA_DIR}/uploads ${GITLAB_INSTALL_DIR}/public/uploads && \
  \
  ### symlink ${GITLAB_INSTALL_DIR}/.secret -> ${GITLAB_DATA_DIR}/.secret
  rm -rf ${GITLAB_INSTALL_DIR}/.secret && \
  su-exec git ln -sf ${GITLAB_DATA_DIR}/.secret ${GITLAB_INSTALL_DIR}/.secret && \
  \
  rm -rf ${GITLAB_INSTALL_DIR}/builds && \
  rm -rf ${GITLAB_INSTALL_DIR}/shared && \
  \
  ### install gitlab bootscript, to silence gitlab:check warnings
  cp ${GITLAB_INSTALL_DIR}/lib/support/init.d/gitlab /etc/init.d/gitlab && \
  chmod +x /etc/init.d/gitlab && \
  \
  ### disable default nginx configuration and enable gitlab's nginx configuration
  rm -rf /etc/nginx/conf.d/default.conf

# Configure SSH
RUN sed -i \
  -e "s|^[#]*UsePAM yes|UsePAM no|" \
  -e "s|^[#]*UsePrivilegeSeparation yes|UsePrivilegeSeparation no|" \
  -e "s|^[#]*PasswordAuthentication yes|PasswordAuthentication no|" \
  -e "s|^[#]*LogLevel INFO|LogLevel VERBOSE|" \
  /etc/ssh/sshd_config && \
  echo "UseDNS no" >> /etc/ssh/sshd_config

# Configure git
RUN sudo -u ${GITLAB_USER} git config --global core.autocrlf input && \
  sudo -u ${GITLAB_USER} git config --global gc.auto 0 && \
  sudo -u ${GITLAB_USER} git config --global repack.writeBitmaps true && \
  sudo -u ${GITLAB_USER} git config --global receive.advertisePushOptions true

# Configure sudoers
RUN echo ${GITLAB_USER}" ALL=(root) NOPASSWD: /usr/sbin/sshd >/etc/sudoers.d/git" && \
  rm -rf "${GITLAB_HOME}/.ssh" && \
  ln -sf "${GITLAB_DATA_DIR}/.ssh" "${GITLAB_HOME}/.ssh"

# Cleanup
RUN apk del --purge .gitlab-build-deps && \
  rm -rf ${GITLAB_INSTALL_DIR}/node_modules && \
  # rm -rf ${GITLAB_HOME}/.bundle && \
  # rm -rf ${GITLAB_HOME}/.cache && \
  # rm -rf ${GITLAB_HOME}/.yarn && \
  #rm -rf ${GITLAB_INSTALL_DIR}/.git && \
  # rm -rf ${GITLAB_INSTALL_DIR}/docker* && \
  # rm -rf ${GITLAB_INSTALL_DIR}/qa && \
  #rm -rf ${GITLAB_GITALY_INSTALL_DIR}/.git && \
  rm -rf ${GITLAB_GITALY_INSTALL_DIR}/*.md && \
  rm -rf ${GITLAB_GITALY_INSTALL_DIR}/Dockerfile && \
  rm -rf ${GITLAB_GITALY_INSTALL_DIR}/Makefile && \
  rm -rf ${GITLAB_WORKHORSE_INSTALL_DIR}/_build && \
  #rm -rf ${GITLAB_WORKHORSE_INSTALL_DIR}/.git && \
  rm -rf ${GITLAB_WORKHORSE_INSTALL_DIR}/testdata && \
  rm -rf ${GITLAB_PAGES_INSTALL_DIR}/.git && \
  rm -rf /usr/local/bundle/cache && \
  rm -rf /usr/share/vim/vim80/doc/* && \
  # rm -rf /usr/src/* && \
  rm -rf /var/cache/apk/*

ENV EXECJS_RUNTIME "Disabled"

# Entrypoint Configuration
WORKDIR ${GITLAB_INSTALL_DIR}

# Network Configuration
EXPOSE 22/tcp 80/tcp 443/tcp

# Add Assets
ADD install /

# S6 sctipts permissions
RUN set -x && \
  chmod -R u+x /etc/s6 && \
  chmod -R u+x /etc/cont-init.d
