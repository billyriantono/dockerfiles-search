FROM odisee/web-base-php7-ldap:latest
MAINTAINER Kim Van Melckebeke <kim.vanmelckebeke@odisee.be>

# Install varioius utilities
RUN yum -y install php-xdebug

# Override xdebug config
ADD 15-xdebug.ini /etc/php.d/15-xdebug.ini