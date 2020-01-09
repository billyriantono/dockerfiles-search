FROM centos:7
LABEL version="1.0"
LABEL description="kcshop setup"

# install php env
WORKDIR /root/src/
RUN yum install -y wget vim net-tools screen git openssl
COPY lnmp1.5.tar.gz /root/src/lnmp1.5.tar.gz
RUN tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && LNMP_Auto="y" DBSelect="9" DB_Root_Password="0220f96dba" InstallInnodb="y" PHPSelect="8" SelectMalloc="1" ./install.sh lnmp

# install Imagick
#RUN wget http://file.kcshop.pro/ImageMagick-7.0.7-25.tar.gz && tar zxvf ImageMagick-7.0.7-25.tar.gz && cd ImageMagick-7.0.7-25 && ./configure && make && make install && cd .. && wget http://file.kcshop.pro/imagick-3.4.3.tgz && tar zxvf imagick-3.4.3.tgz && cd imagick-3.4.3 && /usr/local/php/bin/phpize && ./configure --with-php-config=/usr/local/php/bin/php-config && make && make install && sed -i '/\[PHP\]/a\extension=imagick\.so' /usr/local/php/etc/php.ini	&& sed -i "s/^fastcgi_param PHP_ADMIN_VALUE/#&/" /usr/local/nginx/conf/fastcgi.conf;
