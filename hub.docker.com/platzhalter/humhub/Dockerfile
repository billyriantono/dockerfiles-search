FROM debian

WORKDIR /opt
RUN apt update && apt install -y apache2 libapache2-mod-php5 wget php5-gd php5-intl php5-curl php5-mysql php5-sqlite && \
	wget "https://www.humhub.org/de/download/default/start?version=1.1.1&type=tar.gz&ee=0" -O humhub.tar.gz && \
	mkdir /var/humhub && tar zxvf humhub.tar.gz -C /var/humhub/ --strip-components 1 && rm -rf * && chmod 777 /var/humhub/ -R && chown www-data:www-data /var/humhub/ -R && \
	a2enmod rewrite
COPY start.sh /opt/start.sh
COPY apache.conf /etc/apache2/sites-available/000-default.conf
RUN chmod +x /opt/start.sh

EXPOSE 80

ENTRYPOINT /opt/start.sh
