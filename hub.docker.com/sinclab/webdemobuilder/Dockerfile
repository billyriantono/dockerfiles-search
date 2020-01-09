FROM php:5.5-apache
MAINTAINER Milton Pividori <mpividori@sinc.unl.edu.ar>

#ENV DOCKER_HOST="tcp://docker:2375"
ENV webdemo_branch="default"
ENV WDB_HG_REPO="/app"
ENV WDB_PHP_DIR="${WDB_HG_REPO}/webdemobuilder"
ENV WDB_AUTH_FILE="${WDB_HG_REPO}/webdemo.pwd"
ENV WDB_USER_PASSWORD=""


# Check that HTTPS transport is available to APT
RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update && apt-get install -y --no-install-recommends \
    apt-transport-https \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*


# Docker repository for Apt
RUN apt-key adv \
  --keyserver hkp://p80.pool.sks-keyservers.net:80 \
  --recv-keys 58118E89F3A912897C070ADBF76221572C52609D \
  && echo deb https://apt.dockerproject.org/repo debian-jessie main > /etc/apt/sources.list.d/docker.list


# Install web packages
RUN DEBIAN_FRONTEND=noninteractive \
  apt-get update && apt-get install -y --no-install-recommends \
    docker-engine \
    mercurial \
    sudo \
    zlib1g-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && docker-php-ext-install zip


# Clone repository
COPY hgrc /root/.hgrc
RUN hg clone https://bitbucket.org/sinc-lab/webdemobuilder ${WDB_HG_REPO} \
  && hg update ${webdemo_branch} -R ${WDB_HG_REPO}


# Update the default apache site with the config we created.
RUN echo "ServerSignature Off" >> /etc/apache2/apache2.conf \
  && echo "ServerTokens Prod" >> /etc/apache2/apache2.conf

COPY htaccess ${WDB_PHP_DIR}/.htaccess
RUN rm -rf /var/www/html && ln -s ${WDB_PHP_DIR} /var/www/html

# PHP config (customized)
COPY php.ini /usr/local/etc/php/


# Make www-data user able to run docker
RUN echo "www-data ALL=(ALL) NOPASSWD: /usr/bin/docker" >> /etc/sudoers.d/www-data


# By default, simply start apache.
COPY start.sh /
ENTRYPOINT ["/start.sh"]
CMD [""]

