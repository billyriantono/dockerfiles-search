FROM ubuntu:18.04
LABEL MAINTAINER="Jorge Coll <jorge_coll@hotmail.com>"
ENV DEBIAN_FRONTEND=noninteractive 
RUN apt-get update && \
        apt-get install -y apache2 && \
        apt-get install -y php libapache2-mod-php  php-mysql php-gd && \
        ln -sf /dev/stderr /var/log/apache2/error.log && \
        ln -sf /dev/stdout /var/log/apache2/access.log && \
        echo "<html><body><hr/><h1>Hola Apache/php en Docker</h1> <hr/>" > /var/www/html/info.php && \
        echo " <?php  phpinfo(); ?></body></html>" >> /var/www/html/info.php
EXPOSE 80
ENTRYPOINT ["/usr/sbin/apachectl", "-D", "FOREGROUND"]    
    
