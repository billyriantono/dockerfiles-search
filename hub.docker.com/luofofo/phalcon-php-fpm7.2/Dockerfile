FROM php:7.2-fpm

# fork from phalconphp/php-fpm:7.2-min

# 本dockerfiles增加的項目如下
# git
# php-mongodb
# php-memcached
# php-solr
# php-gd
# php-exif
# php-mbstring
# php-zip 給composer安裝的時候，不要去clone git repo，導致vendor裡面有.git資料夾
# composer

# 注意，這邊不能用 phpenmod，要用docker-php-ext-enable
# 注意，安裝php extention 用 docker-php-ext-install
# git libxml2 libxml2-dev libcurl4-gnutls-dev 這個是為了要安裝php solr
# zlib1g-dev 這個是為了要安裝memcahced
# libpng-dev 為了要安裝gd

RUN apt update \
&& apt install -y git zip \
&& git clone --depth=1 --branch 3.4.x --single-branch "git://github.com/phalcon/cphalcon.git" \
&& cd cphalcon/build \
&& ./install \
&& cp ../tests/_ci/phalcon.ini $(php-config --configure-options | grep -o "with-config-file-scan-dir=\([^ ]*\)" | awk -F'=' '{print $2}') \
&& cd ../../ \
&& rm -r cphalcon \
&& apt install -y git libxml2-dev libcurl4-gnutls-dev zlib1g-dev libmemcached-dev libpng-dev\
&& pecl install mongodb memcached\
&& docker-php-ext-install gd exif mbstring zip\
&& docker-php-ext-enable mongodb memcached gd exif mbstring zip\
&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer\
&& cd /tmp\
&& git clone https://github.com/php/pecl-search_engine-solr.git\
&& cd pecl-search_engine-solr\
&& phpize\
&& ./configure\
&& make\
&& make install\
&& rm -rf /tmp/pecl-search_engine-solr\
&& docker-php-ext-enable solr \
&& apt clean \
&& rm -rf /var/lib/apt/lists/* \
&& pecl clear-cache
