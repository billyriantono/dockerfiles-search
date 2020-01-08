FROM djocker/linuxbrew as builder
LABEL maintainer="Sergey Cherepanov <s@cherepanov.co>"
LABEL name="djocker/php"
ARG DEBIAN_FRONTEND=noninteractive
ARG PHP_FORMULA=php74
ARG HOMEBREW_NO_INSTALL_CLEANUP=1
ARG HOMEBREW_NO_AUTO_UPDATE=1

RUN brew update \
    && brew cleanup \
    && brew tap djocker/php

RUN brew install --build-from-source --only-dependencies ${PHP_FORMULA}
RUN brew install --build-from-source ${PHP_FORMULA} && php -v
RUN brew install ${PHP_FORMULA}-intl ${PHP_FORMULA}-mcrypt ${PHP_FORMULA}-apcu ${PHP_FORMULA}-opcache ${PHP_FORMULA}-tidy ${PHP_FORMULA}-imagick
RUN brew install ${PHP_FORMULA}-pdo-pgsql ${PHP_FORMULA}-mongodb ${PHP_FORMULA}-redis
RUN brew install ${PHP_FORMULA}-xhprof ${PHP_FORMULA}-memprof ${PHP_FORMULA}-xdebug
RUN brew install node
RUN brew install yarn
RUN brew install composer

# Cleanup
RUN brew remove autoconf perl berkeley-db python@2 \
    && rm -rf /home/linuxbrew/.cache/Homebrew \
    && brew cleanup \
    && rm -rf /home/linuxbrew/.linuxbrew/Homebrew/Library/Homebrew/vendor/portable-ruby

FROM djocker/debian
RUN useradd -m -s /bin/bash linuxbrew
USER linuxbrew
WORKDIR /home/linuxbrew
ENV PATH=/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH \
    SHELL=/bin/bash \
    HOMEBREW_NO_AUTO_UPDATE=1 \
    HOMEBREW_NO_INSTALL_CLEANUP=1
COPY --from=builder --chown=linuxbrew:linuxbrew /home/linuxbrew /home/linuxbrew