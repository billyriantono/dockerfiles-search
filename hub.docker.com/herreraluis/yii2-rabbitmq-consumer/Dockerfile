FROM debian:jessie

RUN apt-get update
RUN apt-get install -y  nano wget
RUN echo 'deb http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list
RUN echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list
RUN wget https://www.dotdeb.org/dotdeb.gpg
RUN apt-key add dotdeb.gpg
RUN apt-get update
RUN apt-get install -y apache2 php7.0 php7.0-mysql php7.0-bcmath unzip
RUN a2enmod rewrite
COPY apache2.conf /etc/apache2/
COPY 000-default.conf /etc/apache2/sites-available/
COPY project.zip /opt/
COPY script.sh /opt/
RUN usermod -u 1000 www-data
COPY start.sh /opt/
RUN chmod +x /opt/start.sh

CMD ["/opt/start.sh"]

EXPOSE 80 443
