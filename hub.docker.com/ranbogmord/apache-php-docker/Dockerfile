FROM ubuntu:16.04
MAINTAINER John Eriksson <root@ranbogmord.com>

RUN apt-get update && apt-get install -y apache2 curl php libapache2-mod-php php-mcrypt php-mysql php-gd php-intl php-mbstring

RUN systemctl disable apache2

CMD ["apache2ctl", "-D", "FOREGROUND"]

