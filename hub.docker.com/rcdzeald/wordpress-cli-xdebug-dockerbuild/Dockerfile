#
# Installs WordPress with wp-cli (wp.cli.org) and xdebug installed
# Docker Hub:
# Github Repo: https://github.com/Zeald/core.wordpress-cli-xdebug-dockerbuild

FROM wordpress:latest
LABEL maintainer Raymund C. Delfin <raymund.delfin@zeald.com>

# Add sudo in order to run wp-cli as the www-data user
RUN apt-get update && apt-get install -y sudo less

# Add WP-CLI
RUN curl -o /bin/wp-cli.phar https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
COPY wp-su.sh /bin/wp
RUN chmod +x /bin/wp-cli.phar /bin/wp

# Cleanup
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG XDEBUGPORT
ENV XDEBUG_PORT if [[ -z "$XDEBUG_PORT" ]]; then \
    echo 9000 \
else \
  echo $XDEBUGPORT \
if

RUN yes | pecl install xdebug && \
  echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini && \
  echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini && \
  echo "xdebug.remote_autostart=on" >> /usr/local/etc/php/conf.d/xdebug.ini