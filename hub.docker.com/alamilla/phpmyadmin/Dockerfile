# phpmyadmin
#
# VERSION               1.0

FROM     alamilla/apache2-php
MAINTAINER Andres F. Lamilla, "alamilla@gmail.com"

# se actualiza la base de datos de apt
RUN apt-get update -qq #21/07/2014

# instalacion de los paquetes necesarios para la app
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-client php5-curl php5-mysql php5-mcrypt php5-gd php-apc

# Configuracion phpmyadmin
RUN cd /tmp && wget http://sourceforge.net/projects/phpmyadmin/files/latest/download -O phpmyadmin.zip && unzip -q phpmyadmin.zip && rm phpmyadmin.zip && mv php* /opt/phpmyadmin
ADD src/config.inc.php /opt/phpmyadmin/

# se modifica el directorio /var/www/html
RUN rm -rf /var/www/html
RUN ln -s /opt/phpmyadmin/ /var/www/html

# Configuracion apache
RUN echo "ServerName localhost" > /etc/apache2/conf-available/fqdn.conf
RUN a2enconf fqdn
RUN a2enmod rewrite

# se adicionan los archivos template de configuracion
ADD src/run.sh /usr/local/bin/run.sh
RUN chmod +x /usr/local/bin/*.sh

EXPOSE 80
CMD ["/usr/local/bin/run.sh"]
