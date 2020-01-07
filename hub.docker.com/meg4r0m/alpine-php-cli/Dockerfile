FROM meg4r0m/docker-alpine-php:latest

LABEL php.version=7.2
LABEL maintainer="Florian Durano <psykoterro@gmail.com>" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.vendor="meg4r0m" \
    org.label-schema.name="php-cli-alpine" \
    org.label-schema.description="small php-cli image based on alpine" \
    org.label-schema.vcs-url="https://github.com/psykoterro/docker-php-cli-alpine"

# Environments
ARG DOCKER_TIMEZONE=Europe/Paris
ARG DOCKER_LOCALE=fr_FR.UTF-8

# Configure timezone
# -----------------------------------------------------------------------------
RUN apk add --update tzdata && \
	cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" > /etc/timezone

# Base packages
# Java (used for eg. eZTika indexing)
# poppler-utils used for pdftotext binary (note that eztika is a much better option!)
# Mysql client, useful for db dumps and such
# -----------------------------------------------------------------------------
RUN echo "@edge-main http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \ 
    && echo "@edge-community http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

RUN apk add --update && \
    apk add --no-cache wget \
    bash-completion \
    netcat-openbsd \
    git \
    pwgen \
    sudo \
    unzip \
    vim \
    nano \
    mysql-client \
    imagemagick \
    jpegoptim \
    poppler-utils \
    openjdk7-jre \
    curl

# Install language pack
RUN apk --no-cache add ca-certificates wget
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-bin-2.28-r0.apk
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-i18n-2.28-r0.apk
RUN apk add glibc-bin-2.28-r0.apk glibc-i18n-2.28-r0.apk glibc-2.28-r0.apk

# Iterate through all locale and install it
# Note that locale -a is not available in alpine linux, use `/usr/glibc-compat/bin/locale -a` instead
COPY ./locale.md /locale.md
RUN cat locale.md | xargs -i /usr/glibc-compat/bin/localedef -i {} -f UTF-8 {}.UTF-8

ENV LC_ALL $DOCKER_LOCALE
ENV LANG $DOCKER_LOCALE
ENV LANGUAGE $DOCKER_LOCALE

# Nodejs global install
# -----------------------------------------------------------------------------
RUN apk add --no-cache nodejs

# Composer global install
# -----------------------------------------------------------------------------
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin && \
    mv /usr/local/bin/composer.phar /usr/local/bin/composer && \
    chmod 755 /usr/local/bin/composer

# Local user
# -----------------------------------------------------------------------------
RUN mkdir /tmp/profile
COPY conf/.bashrc_append /tmp/profile/.bashrc_append
COPY conf/.gitconfig /tmp/profile/.gitconfig
COPY conf/.vimrc_append /tmp/profile/.vimrc_append

# nb: the 1000 used here for user id and group id is later on replaced by the code in bootstrap.sh...
RUN addgroup -g 1000 site && \
    adduser -S -u 1000 -G site site -h /home/site -s /bin/bash -D -g "" site && \
    sed -i '$ a site   ALL=\(ALL:ALL\) NOPASSWD: ALL' /etc/sudoers

COPY conf/git-completion.bash /home/site/.git-completion.bash
COPY conf/git-prompt.sh /home/site/.git-prompt.sh

RUN cp /etc/skel/.* /home/site/; \
    cat /tmp/profile/.bashrc_append >> /home/site/.bashrc && \
    cat /tmp/profile/.vimrc_append >> /home/site/.vimrc && \
    cp /tmp/profile/.gitconfig /home/site/ && \
    mkdir -p /home/site/.composer && \
    mkdir -p /home/site/.ssh && \
    chown -R site:site /home/site/ && \
    find /tmp/ -type f -name '.*' -maxdepth 1  -delete

# Install fixuid (https://github.com/boxboat/fixuid) to map host user id with container 'site' user id (used in bootstrap.sh)
RUN USER=site && \
    GROUP=site && \
    curl -SsL https://github.com/boxboat/fixuid/releases/download/v0.1/fixuid-0.1-linux-amd64.tar.gz | tar -C /usr/local/bin -xzf - && \
    chown root:root /usr/local/bin/fixuid && \
    chmod 4755 /usr/local/bin/fixuid && \
    mkdir -p /etc/fixuid && \
    printf "user: $USER\ngroup: $GROUP\n" > /etc/fixuid/config.yml

# -----------------------------------------------------------------------------

# Clear archives in cache folder
RUN rm -rf /var/cache/apk/*

ENV PHP_VERSION 7.2.10

COPY bootstrap.sh /run/bootstrap.sh
RUN chmod 755 /run/bootstrap.sh

USER site:site
WORKDIR /home/site/www/

CMD ["/run/bootstrap.sh"]