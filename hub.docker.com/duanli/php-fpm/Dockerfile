FROM ubuntu
#FROM ubuntu:xenial

MAINTAINER duan duan.li@gmail.com

ENV HOME /root
ENV LC_ALL          C.UTF-8
ENV LANG            en_US.UTF-8
ENV LANGUAGE        en_US.UTF-8

#RUN add-apt-repository ppa:ondrej/php  && \
#Run echo "nameserver 192.168.0.250" > /etc/resolv.conf
#RUN "sh" "-c" "echo nameserver 8.8.8.8 >> /etc/resolv.conf"
#RUN echo "deb http://tw.archive.ubuntu.com/ubuntu/ xenial main restricted" > /etc/apt/sources.list
#RUN echo "deb http://tw.archive.ubuntu.com/ubuntu/ xenial main universe" >> /etc/apt/sources.list
#RUN ln -fs /usr/share/zoneinfo/Asia/Taipei /etc/localtime && dpkg-reconfigure -f noninteractive tzdata
RUN ln -fs /usr/share/zoneinfo/Asia/Taipei /etc/localtime
Run apt-get update && apt-get -y install php7.2-fpm php7.2-mysql php7.2-curl php7.2-cli php-pgsql php-ldap php-redis php-mbstring php-xml php7.2-dev php-xdebug php-pear libsasl2-dev supervisor

RUN mkdir -p /usr/local/openssl/include/openssl/ /var/www/html && \
    ln -s /usr/include/openssl/evp.h /usr/local/openssl/include/openssl/evp.h && \
    mkdir -p /usr/local/openssl/lib/ && \
    ln -s /usr/lib/x86_64-linux-gnu/libssl.a /usr/local/openssl/lib/libssl.a && \
    ln -s /usr/lib/x86_64-linux-gnu/libssl.so /usr/local/openssl/lib/

#RUN pecl install mongodb

#RUN echo "extension=mongodb.so" > /etc/php/7.2/fpm/conf.d/20-mongodb.ini && \
#    echo "extension=mongodb.so" > /etc/php/7.2/cli/conf.d/20-mongodb.ini && \
#    echo "extension=mongodb.so" > /etc/php/7.2/mods-available/mongodb.ini

COPY fpm /etc/php/7.2/fpm
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 9000
#ENTRYPOINT service php7.2-fpm start
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
