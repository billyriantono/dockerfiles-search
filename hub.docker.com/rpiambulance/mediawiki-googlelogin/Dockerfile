FROM mediawiki

RUN mkdir /var/www/html/extensions/GoogleLogin
ADD https://extdist.wmflabs.org/dist/extensions/GoogleLogin-master-c628a85.tar.gz /var/www/html/extensions

RUN apt-get update && apt-get install zip unzip
RUN cd /var/www/html/extensions && tar xvzf *.tar.gz -C /var/www/html/extensions
RUN chown -R www-data: /var/www/html/extensions/GoogleLogin

RUN cd /var/www/html/extensions/GoogleLogin && curl https://getcomposer.org/installer | php
RUN cd /var/www/html/extensions/GoogleLogin && php composer.phar update --no-dev
