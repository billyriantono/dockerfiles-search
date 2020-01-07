FROM eclipse/php

ENV DEBIAN_FRONTEND noninteractive

RUN sudo sed -i 's/None/All/g' /etc/apache2/apache2.conf

RUN sudo apt-get update && \
  sudo apt-get install python-software-properties && \
  sudo add-apt-repository ppa:ondrej/php && \
  sudo apt-get update && \
  sudo apt-get purge -y php7.0 php7.0-common && \
  sudo apt-get install -y \
    php7.2-curl \
    php7.2-xml \
    php7.2-zip \
    php7.2-gd \
    php7.2-mysql \
    php7.2-mbstring