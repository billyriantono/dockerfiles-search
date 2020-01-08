FROM phpmyadmin/phpmyadmin
RUN cd /var/www/html
RUN ln -s . phpmyadmin
RUN chown -h www-data:www-data phpmyadmin
ENV PMA_HOST test-mariadb
ENV PMA_PORT 3306
