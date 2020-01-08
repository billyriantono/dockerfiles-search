from php:5-fpm

RUN apt-get update && \
    apt-get install git nginx-full -y

ADD https://s3.amazonaws.com/gitlist/gitlist-master.tar.gz /var/www/
RUN cd           /var/www/                && \
    tar -zxvf     gitlist-master.tar.gz   && \
    mkdir        /var/www/gitlist/cache   && \
    chmod -R 777 /var/www/gitlist

# copy settings to /defaults
RUN mkdir -p       /defaults/conf                             && \
    mv /etc/nginx  /defaults/conf/nginx                       && \
    rm             /defaults/conf/nginx/sites-enabled/default

# RUN test -f /defaults/conf/gitlist/gitlist/config.ini && rm /defaults/conf/gitlist/config.ini

ADD nginx.conf     /defaults/conf/nginx/nginx.conf
ADD root.htpasswd  /defaults/conf/nginx/htpasswd
ADD gitlist.conf   /defaults/conf/nginx/sites-enabled/gitlist.conf
ADD config.ini     /defaults/conf/gitlist/config.ini

# links for shorter volume argument - files are copied there in the entrypoint.sh
RUN mkdir /conf                                                && \
    ln -s /conf/gitlist/config.ini /var/www/gitlist/config.ini && \
    ln -s /conf/nginx              /etc/nginx

ADD entrypoint.sh /entrypoint.sh
CMD /entrypoint.sh
