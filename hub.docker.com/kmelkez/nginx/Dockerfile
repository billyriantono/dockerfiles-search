FROM debian:wheezy
MAINTAINER Matthieu Keromen <sharoomsorg@gmail.com>
ENV REFRESHED_AT 2015-05-22

RUN apt-get update && apt-get install -y wget && \
    echo "deb http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list && \
    echo "deb-src http://packages.dotdeb.org wheezy all" >> /etc/apt/sources.list && \
    wget http://www.dotdeb.org/dotdeb.gpg && apt-key add dotdeb.gpg && \
    apt-get update && apt-get install -y nginx

RUN rm -rf /var/lib/apt/lists/* && \
    unlink /etc/nginx/sites-enabled/default && \	
    chown -R www-data:www-data /var/lib/nginx

EXPOSE 80

ADD ./start.sh /start.sh
RUN chmod 755 /start.sh 

ENTRYPOINT ["/start.sh"]
