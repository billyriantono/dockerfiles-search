FROM debian:stretch-slim

LABEL maintainers="Przemek Szalko <przemek@rentcars.pl>"
ARG DEBIAN_FRONTEND=noninteractive

# basic setup
RUN apt update \
    && apt install -y \
    curl \
    gnupg2 \
    ca-certificates \
    openssh-client \
    git \
    make \
    bzip2 \
    unzip \
    apt-transport-https \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/ \
    && ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime \
    && echo "Europe/Warsaw" > /etc/timezone

# install node and friends
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt install -y nodejs \
    && curl -sL https://yarnpkg.com/install.sh | bash -s -- --version 1.16.0 \
    && ln -s /root/.yarn/bin/yarn /usr/local/bin/yarn \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/

# intall php and utils
RUN curl -so /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
    && sh -c 'echo "deb https://packages.sury.org/php/ stretch main" > /etc/apt/sources.list.d/php.list' \
    && apt-get update \
    && apt update \
    && apt install -y --no-install-recommends \
    php7.2 \
    php7.2-gd php7.2-mysql php7.2-curl php7.2-xml php7.2-mbstring php7.2-zip \
    # required by build-criticalpath (phantomjs)
    libfontconfig \                   
    # required by optimize-images
    pngquant jpegoptim python-scour \ 
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/
    