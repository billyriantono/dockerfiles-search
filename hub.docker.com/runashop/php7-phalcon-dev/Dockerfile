FROM runashop/php7-phalcon:latest

ENV PHALCON_VERSION=3.0.4

# Insall Phalcon Devtools, see https://github.com/phalcon/phalcon-devtools/
RUN set -xe && \
        curl -LO https://github.com/phalcon/phalcon-devtools/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf v${PHALCON_VERSION}.tar.gz && \
        mv phalcon-devtools-${PHALCON_VERSION} /usr/local/phalcon-devtools && \
        ln -s /usr/local/phalcon-devtools/phalcon.php /usr/local/bin/phalcon && \
        rm -rf v${PHALCON_VERSION}.tar.gz && \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install composer
RUN set -xe && \
        apk add --update git && \
        curl -LO https://getcomposer.org/installer && \
        php installer --quiet && \
        ln -s $(pwd)/composer.phar /usr/local/bin/composer && \
        rm installer