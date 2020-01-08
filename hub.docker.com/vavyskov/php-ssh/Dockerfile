ARG PHP_VERSION=7.2

FROM vavyskov/php:${PHP_VERSION:+${PHP_VERSION}-}apache-stretch

ENV USER_HOME=/var/www
ENV USER_NAME=www-data
ENV USER_PASSWORD=www-data
ENV USER_GROUP=www-data

RUN echo "System tools" \
&&  apt-get update \
&&  apt-get install -y --no-install-recommends \
        git \
        patch \
        wget \
        curl \
        tar \
        zip \
        unzip \
        vim \
        mc \
&&  rm -rf /var/lib/apt/lists/*

RUN echo "Drupal" \
&&  { \
        echo 'export PATH="$PATH:/var/www/html/vendor/bin"'; \
    } > ${USER_HOME}/.bashrc \
&&  chown ${USER_NAME}:${USER_GROUP} .bashrc

## SSH
RUN	apt-get update \
&&	apt-get install -y --no-install-recommends \
        openssh-server \
#        bash \
## Prevents unwanted restarting of the container (when using the docker-compose.yml)
#&&  ssh-keygen -A \
&&  mkdir /var/run/sshd \
&&  rm -rf /var/lib/apt/lists/*

## Configuration
RUN sed -i 's/#PasswordAuthentication/PasswordAuthentication/' /etc/ssh/sshd_config

#groupadd user
#useradd -g user user
##usermod -a -G user user
RUN echo "www-data:www-data" | chpasswd
#RUN echo "${USER_NAME}:${USER_PASSWORD}" | chpasswd
RUN usermod -s /bin/bash www-data
#RUN usermod -s /bin/bash ${USER_NAME}



## Multi-services
RUN	apt-get update \
&&  apt-get install -y --no-install-recommends \
        supervisor \
&&  rm -rf /var/lib/apt/lists/*
COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

#COPY config/supervisord.conf /
#ENTRYPOINT ["supervisord", "-c", "/supervisord.conf"]



## Initialize container
#COPY config/entrypoint.sh /usr/local/bin/
#RUN chmod u+x /usr/local/bin/entrypoint.sh
#ENTRYPOINT ["entrypoint.sh"]



CMD ["/usr/bin/supervisord"]
