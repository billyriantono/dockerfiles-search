FROM fabrizzio/docker-php-oci8:latest
MAINTAINER Dieter Provoost <dieter.provoost@marlon.be>

# Install apache
RUN apt-get -y -f install apache2 libapache2-mod-php5

RUN a2dissite 000-default
RUN a2enmod rewrite

RUN rm -rf /etc/php5/apache2
RUN ln -s /etc/php5/cli /etc/php5/apache2

RUN apt-get clean -y

EXPOSE 22
EXPOSE 80

ADD start.sh start.sh

CMD ["sh", "start.sh"]

