FROM mrchimp/alpine-nginx-base

RUN apk add --update php-mcrypt php-openssl php-curl php-json php-dom php-pdo php-zip php-mysql php-bcmath php-gd php-pdo_mysql  php-xmlreader php-xmlrpc php-bz2 php-memcache php-fpm

# Fix permissions 
#RUN chown -Rf root:nobody /etc/nginx/html/

#Copy the nginx file
COPY nginx.conf /etc/nginx/conf/nginx.conf

#Copy the php ini file
COPY php.ini /etc/php/php.ini

#Copy php info to html directory
COPY index.php /etc/nginx/html/index.php

#Run php-FPM
#RUN /usr/bin/php-fpm

#Copy start script
COPY run.sh /start.sh
RUN chmod 755 /start.sh

#CMD ["nginx", "-g", "daemon off;"]
ENTRYPOINT /start.sh
