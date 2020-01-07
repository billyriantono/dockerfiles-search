# This image contains apache server with php and php5-curl

FROM eboraas/apache-php
MAINTAINER Luka Stosic <lstosic@infodation.nl>

RUN apt-get update && apt-get -y install php5-curl

# Remove default index.html
RUN rm -f /var/www/html/index.html

EXPOSE 80
