FROM debian

WORKDIR /opt
RUN apt-get update && apt-get install -y apache2 libapache2-mod-php5 php5 wget tar php5-mysql bzip2 php5-gd php5-curl
RUN wget https://download.nextcloud.com/server/releases/nextcloud-10.0.1.tar.bz2
RUN mkdir /var/nextcloud && tar xvjf nextcloud-10.0.1.tar.bz2 -C /var/nextcloud --strip-components 1
RUN rm -rf *
COPY start.sh /opt/start.sh
COPY apache.conf /etc/apache2/sites-available/000-default.conf
COPY php.ini /etc/php5/apache2/php.ini
RUN a2enmod rewrite
RUN chmod +x /opt/start.sh
RUN chmod 777 -R /var/nextcloud

EXPOSE 80

ENTRYPOINT /opt/start.sh
