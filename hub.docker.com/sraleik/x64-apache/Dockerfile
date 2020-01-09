#docker build -t sraleik/x64-apache .
#docker run -d -p 80:80 -e ALLOW_OVERRIDE=true -v /var/run/mysqld/mysqld.sock:/var/run/mysqld/mysqld.sock --name soma-apache sraleik/x64-apache:trusty
FROM sraleik/x64-ubuntu:trusty
MAINTAINER Sraleik <sraleik@gmail.com>

# Install dépendance

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -yq install \
        curl \
        apache2 \
        libapache2-mod-php5 \
        php5-mysql \
        php5-mcrypt \
        php5-gd \
        php5-curl \
        php-pear \
        jq \
        mysql-client \
        php-apc && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN /usr/sbin/php5enmod mcrypt
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf && \
    sed -i "s/variables_order.*/variables_order = \"EGPCS\"/g" /etc/php5/apache2/php.ini

ENV ALLOW_OVERRIDE **False**

# Configure /app folder with default app
RUN mkdir -p /app && rm -fr /var/www/html && ln -s /app /var/www/html
ADD app/* /app/
# Add image configuration and scripts
ADD run.sh /run.sh
RUN chmod 755 /*.sh

EXPOSE 80
WORKDIR /app
CMD ["/run.sh"]
