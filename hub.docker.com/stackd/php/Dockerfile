FROM tutum/apache-php

COPY run.sh /
RUN chmod +x /run.sh

RUN sed -i "s/AllowOverride None/AllowOverride All/g" /etc/apache2/apache2.conf && \
    sed -i "s/post_max_size = .*/post_max_size =  32M/g" /etc/php5/apache2/php.ini && \
    sed -i "s/upload_max_filesize = .*/upload_max_filesize =  32M/g" /etc/php5/apache2/php.ini

RUN a2enmod rewrite
