FROM wptestlabs/php7fpm-wpmin
#  This image (built) is on hub.docker.com as wptestlabs/php7fpm-wpcli

ADD  https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar /bin/wp-cli.phar
RUN  mv /bin/wp-cli.phar /bin/wp && chmod +x /bin/wp;

#   -F  -- Force to stay in Foreground ie Don't Deamonize
CMD ["/usr/sbin/php-fpm7", "-F"]
