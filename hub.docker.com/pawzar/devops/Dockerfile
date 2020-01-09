FROM php:fpm

ARG COMPOSER_HASH="93b54496392c062774670ac18b134c3b3a95e5a5e5c8f1a9f115f203b75bf9a129d5daa8ba6a13e2cc8a1da0806388a8"

ARG NODE_VERSION="10.9.0"
ARG YARN_VERSION="1.9.4"

ARG USER_NAME="dev"
ARG USER_UID="1000"
ARG USER_GID="1000"

ENV TERM xterm
ENV LOCALTIME Europe/Warsaw

# update
RUN apt-get -q update \
    && apt-get -qyf --no-install-recommends install \
        apt-utils vim less dnsutils bash-completion net-tools \
        nmap mtr curl git bzip2 zip unzip tree mc wget \
        openssl openssh-client openssh-server \
        gnupg2 dirmngr connect-proxy \
        libpng-dev \
        mysql-client zsh \
# bz2
        libbz2-dev \
# curl
        libcurl3-dev \
    && apt-get -qy autoremove && apt-get -qy clean all \
    && rm -rf /var/lib/apt/lists/* /var/cache/apk/* /usr/share/doc/*

RUN docker-php-ext-install bz2 curl mysqli bcmath mbstring pdo_mysql

# sshd config
RUN mkdir /var/run/sshd
RUN sed "s|#PasswordAuthentication\s*yes|PasswordAuthentication no|g" /etc/ssh/sshd_config
RUN sed "s|session\s*required\s*pam_loginuid.so|session optional pam_loginuid.so|g" -i /etc/pam.d/sshd

# xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# timezone (FIXME: This seems to be redundant)
RUN ln -sf /usr/share/zoneinfo/$LOCALTIME /etc/localtime
RUN echo "date.timezone = \"${LOCALTIME}\"" | tee --append $PHP_INI_DIR/conf.d/00-default.ini

# composer
RUN wget https://getcomposer.org/installer --quiet --output-document=/tmp/composer-setup.php \
    &&         echo "  expected: $COMPOSER_HASH" \
    && php -r "echo 'calculated: '. hash_file('SHA384','/tmp/composer-setup.php').PHP_EOL;" \
    && php -r "exit(strcmp(hash_file('SHA384','/tmp/composer-setup.php'),getenv('COMPOSER_HASH')));" \
    && php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && rm /tmp/composer-setup.php

# gpg keys listed at https://github.com/nodejs/node#release-team
RUN set -ex \
  && for key in \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 \
    56730D5401028683275BD23C23EFEFE93C4CFFFE \
    77984A986EBC2AA786BC0F66B01FBB92821C587A \
    8FCCA13FEF1D0C2E91008E09770F7A9A5AE15600 \
  ; do \
    gpg --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys "$key" || \
    gpg --keyserver hkp://ipv4.pool.sks-keyservers.net --recv-keys "$key" || \
    gpg --keyserver hkp://pgp.mit.edu:80 --recv-keys "$key" ; \
  done

RUN ARCH= && dpkgArch="$(dpkg --print-architecture)" \
  && case "${dpkgArch##*-}" in \
    amd64) ARCH='x64';; \
    ppc64el) ARCH='ppc64le';; \
    s390x) ARCH='s390x';; \
    arm64) ARCH='arm64';; \
    armhf) ARCH='armv7l';; \
    i386) ARCH='x86';; \
    *) echo "unsupported architecture"; exit 1 ;; \
  esac \
  && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH.tar.xz" \
  && curl -fsSLO --compressed "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
  && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
  && grep " node-v$NODE_VERSION-linux-$ARCH.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
  && tar -xJf "node-v$NODE_VERSION-linux-$ARCH.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
  && rm "node-v$NODE_VERSION-linux-$ARCH.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN set -ex \
  && for key in \
    6A010C5166006599AA17F08146C2130DFD2497F5 \
  ; do \
    gpg --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys "$key" || \
    gpg --keyserver hkp://ipv4.pool.sks-keyservers.net --recv-keys "$key" || \
    gpg --keyserver hkp://pgp.mit.edu:80 --recv-keys "$key" ; \
  done \
  && curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz" \
  && curl -fsSLO --compressed "https://yarnpkg.com/downloads/$YARN_VERSION/yarn-v$YARN_VERSION.tar.gz.asc" \
  && gpg --batch --verify yarn-v$YARN_VERSION.tar.gz.asc yarn-v$YARN_VERSION.tar.gz \
  && mkdir -p /opt \
  && tar -xzf yarn-v$YARN_VERSION.tar.gz -C /opt/ \
  && ln -s /opt/yarn-v$YARN_VERSION/bin/yarn /usr/local/bin/yarn \
  && ln -s /opt/yarn-v$YARN_VERSION/bin/yarnpkg /usr/local/bin/yarnpkg \
  && rm yarn-v$YARN_VERSION.tar.gz.asc yarn-v$YARN_VERSION.tar.gz

# skel
COPY skel /etc/skel/
RUN chmod u+rwX,go-rwx -R /etc/skel/

# root
#RUN sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
COPY skel /root/
RUN chmod u+rwX,go-rwx -R /root/

# group
RUN groupmod --non-unique --gid $USER_GID www-data

# user
RUN useradd \
    --uid $USER_UID \
    --no-user-group --gid $USER_GID \
    --create-home \
    --shell /bin/bash \
    $USER_NAME

# scripts
COPY bin /usr/local/bin/

ENTRYPOINT ["docker-php-entrypoint.sh"]
CMD ["php-fpm"]
