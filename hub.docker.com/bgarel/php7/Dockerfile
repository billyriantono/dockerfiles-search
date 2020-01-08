FROM bgarel/apache
MAINTAINER Benjamin GAREL <bgarel@hotmail.com>

RUN apt-get update && apt-get -y install php7.0 libapache2-mod-php7.0 && rm -rf /var/lib/apt/lists/*

EXPOSE 80 

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]