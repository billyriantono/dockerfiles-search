FROM ubuntu:16.04
MAINTAINER Kevin Park<kevinpark@webace.co.kr>

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install openssl
RUN apt-get -y install apache2
RUN apt-get -y install php libapache2-mod-php php-xml

ADD start.sh /start.sh
RUN chmod +x /start.sh

EXPOSE 443 80

CMD ["/start.sh"]
