FROM ubuntu:18.04

MAINTAINER Stanislav Vitkovskiy <stas.vitkovsky@gmail.com>

# Packages required by tt-rss
RUN apt-get -q update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y -q \
        php7.2-common \
        php7.2-fpm \
        php7.2-pgsql \
        php7.2-xml \
        php7.2-json \
        php7.2-mbstring \
        php7.2-gd \
        nginx-light \
        ca-certificates \
        curl && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Installing tt-rss master branch
RUN curl -s -L -o - https://git.tt-rss.org/git/tt-rss/archive/master.tar.gz | \
        tar -xz -C /var/www/ --strip-components=1 && \
    mv /var/www/config.php-dist /var/www/config.php && \
    rm -rf /var/www/install && \
    chown -R www-data.www-data /var/www/

# Installing tt-rss feedly theme master branch
RUN curl -s -o - https://codeload.github.com/levito/tt-rss-feedly-theme/tar.gz/master | \
        tar -xz -C /var/www/themes/ --strip-components=1 \
            tt-rss-feedly-theme-master/feedly.css \
            tt-rss-feedly-theme-master/feedly/

# Default settings
ENV TTRSS_DB_HOST=postgres \
    TTRSS_DB_PORT=5432 \
    TTRSS_DB_USER=ttrss \
    TTRSS_DB_NAME=ttrss \
    TTRSS_DB_PASS=ttrss \
    TTRSS_SELF_URL_PATH=http://localhost:8091

# Deploying configuration
COPY etc/ /etc/

# Entrypoint
COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
