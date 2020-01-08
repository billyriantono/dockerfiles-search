FROM centos:6.8

MAINTAINER walkonthemarz@gmail.com

#COPY epel-release-latest-6.noarch.rpm /root
COPY remi-release-6.rpm /root
COPY lib/libImageOperationLib.so /usr/local/lib
COPY lib/libiViewerSDK.so /usr/local/lib


RUN chmod 755 /usr/local/lib/libImageOperationLib.so \
    && yum install -y epel-release \
    && rpm -Uvh /root/remi-release-6.rpm \ 
    && rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro \
    && rpm -Uvh http://li.nux.ro/download/nux/dextop/el6/x86_64/nux-dextop-release-0-2.el6.nux.noarch.rpm \
    && yum --enablerepo=extras install -y wget gcc cmake pkconfig yum-utils python-setuptools centos-release-scl python34 \
    && yum groupinstall -y "Development Tools" \
    && yum install -y libjpeg-turbo libpng libtiff jasper-libs ffmpeg-libs ffmpeg-devel numpy python-devel tbb-devel \
    && wget http://www.ijg.org/files/jpegsrc.v9b.tar.gz -O /root/jpegsrc.v9b.tar.gz \
    && tar -xf /root/jpegsrc.v9b.tar.gz -C /root \
    && cd /root/jpeg-9b && ./configure && make && make install clean \
    && cd /root && echo "/usr/local/lib">> /etc/ld.so.conf && ldconfig \
    && curl -O https://bootstrap.pypa.io/get-pip.py && /usr/bin/python3.4 get-pip.py \
    && pip install supervisor==4.0.2 \
    && rm -rf /root/jpegsrc.v9b.tar.gz \
    && rm -rf /root/jpeg-9b \
    && yum clean all

WORKDIR /root/build
RUN wget https://github.com/Itseez/opencv/archive/2.4.13.6.zip \
    && unzip 2.4.13.6.zip \
    && cd opencv-2.4.13.6 \
    && mkdir release \
    && cd release \
    && cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local .. \
    && make && make install && ldconfig && cd /root && rm -rf /root/build/*

RUN yum-config-manager --enable remi-php71 \
    && yum install -y php php-devel php-fpm php-gmp php-json php-mbstring php-redis php-mcrypt php-mysqlnd php-opcache php-pdo php-pear php-xml php-gd php-intl php-process php-smbclient php-tidy php-recode php-timecop php-soap php-pgsql php-pspell php-snappy php-xmlrpc php-ldap php-imap php-cli php-bcmath php-ast php-embedded php-enchant php-pecl-mailparse php-pecl-uploadprogress php-pecl-swoole4 \
    && yum clean all \
    && mkdir -p /var/www/html/log/
    
COPY php.ini /etc/php.ini
RUN rm -f /etc/localtime \
    && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

#HEALTHCHECK --interval=5s --timeout=3s CMD curl -fs http://localhost || exit 1
EXPOSE 80
CMD []
ENTRYPOINT ["/bin/bash"]
