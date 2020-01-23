FROM liling/phusion-nginx-php5:0.3
MAINTAINER liling@bit.edu.cn

# Install software
RUN apt-get update ; apt-get install -y paps php-pear php5-apcu php5-cli php5-common php5-curl php5-dev php5-fpm php5-gd php5-intl php5-json php5-ldap php5-memcache php5-memcached php5-mongo php5-mysqlnd php5-readline php5-xmlrpc php5-xsl pkg-php-tools ttf-wqy-microhei ttf-dejavu-core ttf-freefont libpango1.0-0 cups-client clamav ; /usr/bin/freshclam ; apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ; mkdir /var/www/moodle; cd /var/www; wget -O - https://bitbucket.org/bitsrv/moodle/get/MOODLE_30_STABLE.tar.bz2 | tar jxf -

# Startup freshclam
RUN mkdir /etc/service/freshclam
ADD services/freshclam.sh /etc/service/freshclam/run
RUN chmod +x /etc/service/freshclam/run
