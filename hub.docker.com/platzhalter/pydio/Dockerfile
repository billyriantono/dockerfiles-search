FROM debian

WORKDIR /opt
RUN apt-get update && apt-get install -y apache2 libapache2-mod-php5 php5 wget tar php5-fpm php5-cli php5-sqlite
RUN wget https://download.pydio.com/pub/core/archives/pydio-core-7.0.2.tar.gz
RUN mkdir /var/pydio && tar zxvf pydio-core-7.0.2.tar.gz -C /var/pydio --strip-components 1
RUN rm -rf *
COPY start.sh /opt/start.sh
COPY apache.conf /etc/apache2/sites-available/000-default.conf
COPY php.ini /etc/php5/apache2/php.ini
RUN a2enmod rewrite
RUN chmod +x /opt/start.sh
RUN chmod 777 -R /var/pydio

EXPOSE 80

ENTRYPOINT /opt/start.sh
