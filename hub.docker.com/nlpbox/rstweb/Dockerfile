FROM nlpbox/nlpbox-base:16.04

RUN apt-get update -y && apt-get upgrade -y && \
    apt-get install python-pip phantomjs apache2 elinks -y && \
    pip2 install cherrypy selenium

WORKDIR /var/www/html
RUN git clone https://github.com/amir-zeldes/rstWeb.git && \
    mv rstWeb rstweb

ADD rstweb.apache.conf /etc/apache2/sites-available/

WORKDIR /etc/apache2/sites-enabled
RUN ln -s ../sites-available/rstweb.apache.conf . && \
    rm 000-default.conf && \
    a2enmod rewrite && service apache2 restart && \
    a2enmod cgi && service apache2 restart && \
    chown -R www-data:www-data /var/www/html/rstweb && \
    chmod -R ug+rwx /var/www/html/rstweb && \
    usermod -aG www-data root && \
    newgrp www-data && \
    service apache2 restart

EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND
