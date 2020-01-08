FROM miyamotota/centos67-base:latest

MAINTAINER miyamoto_ta <miyamoto_ta@zoho.com>

RUN yum install -y epel-release
RUN wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN rpm -Uvh remi-release-6*.rpm
RUN yum --enablerepo=remi-php70 update php\*
RUN yum --enablerepo=remi-php70,epel install -y php php-cli php-devel php-common php-mbstring php-mysql php-pecl-xdebug php-fpm php-gd php-gmp php-mcrypt php-opcache php-pdo php-xml php-mbstring

RUN yum -y install zlib-devel cyrus-sasl-devel
RUN wget https://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz
RUN tar xvf libmemcached-1.0.18.tar.gz
RUN cd libmemcached-1.0.18 && \
./configure && \
make && \
make install
RUN git clone https://github.com/php-memcached-dev/php-memcached -b php7
RUN cd php-memcached && \
phpize && \
./configure && \
make && \
make install

COPY ./etc/php-fpm.d/www.conf /etc/php-fpm.d/
COPY ./etc/php.d/memcached.ini /etc/php.d/

EXPOSE 9000
EXPOSE 9001
CMD ["php-fpm", "--nodaemonize"]
