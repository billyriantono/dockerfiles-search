FROM debian:buster

RUN apt-get update -yq \
&& apt-get install curl php7.3 git software-properties-common -yq \
&& curl -sL https://deb.nodesource.com/setup_11.x | bash \
&& apt-get install nodejs -yq

RUN npm i -g auth0-deploy-cli

ENV COMPOSER_ALLOW_SUPERUSER 1

RUN curl -o /tmp/composer-installer https://getcomposer.org/installer && \
  curl -o /tmp/composer-installer.sig https://composer.github.io/installer.sig &&  \
  php -r "if (hash('SHA384', file_get_contents('/tmp/composer-installer')) !== trim(file_get_contents('/tmp/composer-installer.sig'))) { unlink('/tmp/composer-installer'); echo 'Invalid installer' . PHP_EOL; exit(1); }" && \
  php /tmp/composer-installer --version=1.8.4 --filename=composer --install-dir=/usr/local/bin && \
  php -r "unlink('/tmp/composer-installer');" && \
  php -r "unlink('/tmp/composer-installer.sig');"

COPY . /usr/local/src/sif
RUN cd /usr/local/src/sif && \
  composer install && \
  ln -s /usr/local/src/sif/bin/sif /usr/local/bin/sif && \
  ln -s /usr/local/src/sif-dev/bin/sif /usr/local/bin/sif-dev
