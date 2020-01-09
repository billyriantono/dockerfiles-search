FROM        debian:wheezy
MAINTAINER  Michael BOUVY <michael.bouvy@gmail.com>

ADD         https://getcomposer.org/composer.phar /usr/local/bin/composer
RUN         chmod +x /usr/local/bin/composer
RUN         apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y upgrade ; \
            DEBIAN_FRONTEND=noninteractive apt-get -y install php5 php5-intl php5-json \ 
            libapache2-mod-php5 git-core php5-curl php5-gd php5-xsl php5-mcrypt supervisor openssh-server

RUN         echo "root:toor" | chpasswd

RUN         mkdir -p /var/run/sshd /var/log/supervisor
            
ADD         supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE      22 80
CMD         ["/usr/bin/supervisord"]
