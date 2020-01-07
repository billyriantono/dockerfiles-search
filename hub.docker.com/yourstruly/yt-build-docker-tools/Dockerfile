FROM debian:stretch-slim
MAINTAINER yourstruly GmbH Hamburg

WORKDIR /app

RUN apt-get update -y && \
    apt-get install -y \
    php php-pear php-curl php-mbstring php-pdo php-intl php-iconv php-gd php-zip\
    curl \
    gnupg \
    git \
    python python-pip \
    ruby ruby-dev

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get install -y nodejs

RUN npm install -g gulp && npm install -g grunt

RUN curl --silent --show-error https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer && chmod a+x /usr/bin/composer

RUN pip install awscli --upgrade --user

RUN echo "export PATH=~/.local/bin:$PATH" > ~/.bash_profile && export PATH=~/.local/bin:$PATH

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash \
 && export NVM_DIR="$HOME/.nvm" \
 && . $NVM_DIR/nvm.sh \
 && nvm install 6 \
 && nvm install 8 \
 && nvm install 10

RUN gem install sass