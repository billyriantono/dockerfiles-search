FROM gsdiniz/php-docker:latest

ARG WP_VERSION=5.2.2

RUN wget -O /tmp/wp.tar.gz https://br.wordpress.org/wordpress-${WP_VERSION}-pt_BR.tar.gz

WORKDIR /tmp
RUN tar -xzf wp.tar.gz

USER www-data
WORKDIR /var/www/html/
RUN cp /tmp/wordpress/* . -R
RUN rm -rf /tmp/wordpress && \
    rm -rf /tmp/wp.tar.gz

ADD ./themes wp-content/themes
ADD ./plugins wp-content/plugins