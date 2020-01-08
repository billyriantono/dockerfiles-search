FROM tutum/apache-php
RUN sed -ni '1h;1!H;${g;s/<Directory \/var\/www\/>.*<\/Directory>/<Directory \/var\/www\/>\n\tOptions Indexes FollowSymLinks\n\tAllowOverride All\n\tRequire all granted\n<\/Directory>/;p;}' /etc/apache2/apache2.conf
RUN a2enmod rewrite


# Configure user nobody to match unRAID's settings
 RUN \
 usermod -u 99 nobody && \
 usermod -g 100 nobody && \
 usermod -d /home nobody && \
 chown -R nobody:users /home
