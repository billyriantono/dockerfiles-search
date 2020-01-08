FROM eboraas/apache 
ADD vhost.conf /etc/apache2/
ADD index.html /var/www/html/
RUN echo "Include vhost.conf" >> /etc/apache2/apache2.conf
RUN service apache2 restart

