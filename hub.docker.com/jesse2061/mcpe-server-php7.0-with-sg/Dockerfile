FROM debian

#RUN echo \
#    deb http://mirrors.aliyun.com/debian/ buster main contrib non-free\
#	\#deb-src http://mirrors.aliyun.com/debian/ buster main contrib non-free\
#	deb http://mirrors.aliyun.com/debian/ buster-updates main contrib non-free\
#	\#deb-src http://mirrors.aliyun.com/debian/ buster-updates main contrib non-free\
#	deb http://mirrors.aliyun.com/debian/ buster-backports main contrib non-free\
#	\#deb-src http://mirrors.aliyun.com/debian/ buster-backports main contrib non-free\
#	deb http://mirrors.aliyun.com/debian-security buster/updates main contrib non-free\
#	\#deb-src http://mirrors.aliyun.com/debian-security buster/updates main contrib non-free\
#   > /etc/apt/sources.list

RUN apt-get update && apt-get install -y \
	autoconf \
	build-essential \
	libssl-dev \
	libxml2-dev \
	wget \
	libzip-dev \
	curl \
	libcurl4-openssl-dev

ENV VERSION 7.0.32
RUN wget -O php-$VERSION.tar.bz2 https://www.php.net/distributions/php-$VERSION.tar.bz2 && tar xjf php-$VERSION.tar.bz2 

RUN cd php-$VERSION \
	&& ./configure \
		--disable-cgi \
		--enable-mbstring \
		--enable-maintainer-zts \
		--enable-zip \
		--enable-bcmath \
		--enable-sockets \
		--with-mhash \
		--with-curl \
		--with-zlib \
		--with-libdir=/lib/x86_64-linux-gnu \
		--with-openssl \
	&& make -j2 \
	&& make install \
	&& cp php.ini-production /usr/local/lib/php.ini \
	&& cd .. \
	&& pecl config-set php_ini /usr/local/lib/php.ini \
	&& pear config-set php_ini /usr/local/lib/php.ini
RUN apt-get install libyaml-dev -y
RUN pecl install yaml
RUN wget https://github.com/krakjoe/pthreads/archive/v3.1.6.tar.gz \
	&& tar -zxvf v3.1.6.tar.gz \
	&& cd pthreads-3.1.6/ \
	&& phpize && ./configure && make && make install

RUN echo "extension=pthreads.so" >> $(php -i | grep "Loaded Configuration File" | awk '{print $5}')


RUN wget https://github.com/crazywhalecc/mcpe-server-docker/raw/master/sg-loader/ixed.7.0ts.lin && mv ixed.7.0ts.lin $(php -i | grep "extensions/no-debug" | awk '{print $3}')/ \
	&& echo "extension=ixed.7.0ts.lin" >> $(php -i | grep "Loaded Configuration File" | awk '{print $5}')

RUN rm php-$VERSION.tar.bz2 \
	&& rm -rf php-$VERSION \
	&& apt-get purge -y autoconf build-essential wget .+-dev \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mkdir /mcserver
WORKDIR /mcserver


CMD bash -c "php server.phar"
