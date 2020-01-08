FROM alpine

RUN apk --no-cache add php5-apache2 php5-pgsql postgresql wget unzip

RUN mkdir /run/apache2/ && chmod 777 /run/apache2/

RUN wget https://github.com/jaguardev/phppgadmin/archive/master.zip && \
    unzip master.zip && \
    rm master.zip && \
    apk del wget unzip && \
    rm -rf /var/www/localhost/htdocs && \
    mv /phppgadmin-master /var/www/localhost/htdocs
    
EXPOSE 80

CMD ["httpd","-D","FOREGROUND"]
