FROM lucasdiedrich/ojs:3.1.1-2

MAINTAINER Matheus Garcia <garcia.figueiredo@gmail.com>

COPY fix_https.sh /var/www/html

WORKDIR /var/www/html

RUN chmod a+x ./fix_https.sh && ./fix_https.sh


