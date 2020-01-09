FROM vpadvance/ora12c

COPY ./src/*.gz /usr/local/src/
COPY ./src/*.rpm /usr/local/src/


RUN yum install -y gcc curl-devel libwebp libwebp-devel gd-devel postgresql-devel sendmail-devel sendmail-cf perl-devel sqlite-devel open-ssl \
        socat openssh-server openssh-clients libssh \
# Install for killall
    && yum install -y psmisc \
# Install nc and sshpass for cvscon2
    && yum install -y nc sshpass \
# Install sudo
    && yum install -y sudo \
# openssl, skip -> already installed from yum
#    && cd /usr/local/src \
#    && tar xvf openssl-0.9.8zg.tar.gz \
#    && cd openssl-* \
#    && ./config --prefix=/usr/local --openssldir=/usr/local/openssl shared \
#    && make;make install \
# MS-SQL
    && cd /usr/local/src \
    && tar zxvf freetds-0.95.tar.gz \
    && cd freetds-* &&  ./configure --prefix=/usr/local/freetds \
    && make;make install \
# What is it?? from Boss
#    &&  mkdir rpm \
#    && cd rpm \
#    && wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm \
#    && rpm -Uvh epel-release-6-8.noarch.rpm \
#    && rpm --import http://oss.oracle.com/ol6/RPM-GPG-KEY-oracle \
#    && rpm -q gpg-pubkey-ec551f03-4c2d256a \
#    && /usr/local/src \
# end of what is it??  
# Apache
    && cd /usr/local/src/ \
    && tar zxvf httpd-2.4.39.tar.gz \
    && cd httpd-2.4.39 \
    && cd srclib \
    && tar zxvf ../../apr-1.7.0.tar.gz \
    && tar zxvf ../../apr-util-1.6.1.tar.gz \
    && mv apr-1.7.0 apr \
    && mv apr-util-1.6.1 apr-util \
    && cd .. \
    && export SSL_BASE=/usr/local/openssl \
    && ./configure --prefix=/usr/local/apache --enable-so --enable-cgi --enable-info --enable-rewrite --enable-speling \
       --enable-usertrack --enable-deflate --enable-ssl --enable-mime-magic --with-included-apr --enable-module=so \
    && make; make install \
# php
    && cd /usr/local/src \
    && tar zxvf php-7.3.6.tar.gz \
    && cd php-7.3.6 \
    && ./configure --with-apxs2=/usr/local/apache/bin/apxs --prefix=/usr/local/apache/php --with-config-file-path=/usr/local/apache/php \
       --disable-cgi --with-zlib --with-gettext --with-gdbm --with-oci8=/opt/oracle/product/12c/dbhome_1/ --with-curl --with-xmlrpc \
       --enable-sigchild --with-pgsql --enable-dba --enable-soap --with-curl=/usr/local/lib --with-gd \
       --with-jpeg-dir=/usr/lib --with-png-dir=/usr/local/lib --with-openssl-dir=/usr/local/openssl --with-openssl --enable-mbstring \
    && make; make install \
# append php into httpd.conf
    && echo 'LoadModule php7_module  modules/libphp7.so' >>/usr/local/apache/conf/httpd.conf \
    && echo 'AddHandler php7-script  .php' >>/usr/local/apache/conf/httpd.conf \
    && echo 'AddType text/html       .php' >>/usr/local/apache/conf/httpd.conf \
    && echo 'AddType application/x-httpd-php-source phps' >>/usr/local/apache/conf/httpd.conf \
    && echo '#Listen localhost:80' >>/usr/local/apache/conf/httpd.conf \
    && echo '#Listen 10.7.8.20:80' >>/usr/local/apache/conf/httpd.conf \
    && echo '#ServerName timest.vpadvance.com:80' >>/usr/local/apache/conf/httpd.conf \
# smarty
    && cd /usr/local \
    && tar zxvf /usr/local/src/smarty-3.1.33.tar.gz \
    && mv smarty-3.1.33 smarty \
# thai alignment
    && cd /usr/local/src \
    && tar xvf libdatrie-0.2.6.tar.gz \
    && cd libdatrie-0.2.6 \
    && ./configure \
    && make;make install \
    && cd /usr/local/src \
    && tar zxvf swath-0.4.3.tar.gz \
    && cd swath-0.4.3 \
    && export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig \
    && ./configure \
    && make;make install \
# OLE-Storage for PERL, Require perl-devel
    && cd /usr/local/src \
    && tar xvf /usr/local/src/OLE-Storage_Lite-0.19.tar.gz \
    && cd OLE-Storage_Lite-0.19 \
    && perl Makefile.PL \
    && make; make install \
# Image Size for PERL, Require perl-devel
    && cd /usr/local/src \
    && tar xvf /usr/local/src/Image-Size-3.300.tar.gz \
    && cd Image-Size-3.300 \
    && perl Makefile.PL \
    && make; make install \ 
# JSON for PERL, Require perl-devel
    && cd /usr/local/src \
    && tar xvf JSON-2.90.tar.gz \
    && cd JSON-2.90 \
    && perl Makefile.PL \
    && make; make install \
# Extract asset
    && cd /usr/local/apache/htdocs \
    && tar zxvf /usr/local/src/assets.tar.gz \
    && chown -Rf oracle:oinstall assets \
# Support fpdf
    && cd /usr/local \
    && tar zxvf /usr/local/src/fpdf16.bin.tar.gz \
    && chown -Rf oracle:oinstall /usr/local/fpdf16 \
# Config sendmail
    && cp /etc/mail/sendmail.mc /etc/mail/sendmail.mc.org \
# Config sudoer
    && echo 'oracle ALL=NOPASSWD: ALL' >>/etc/sudoers \
# Clean Up  
    && rm -f /usr/local/bin/sqlite3;ln -s /usr/bin/sqlite3 /usr/local/bin/sqlite3 \
    && cd /usr/local/src \
    && rm -rf httpd-2.4.39 php-7.3.6 \
    && rm -f /usr/local/src/assets.tar.gz

user oracle

COPY ./conf/php.ini /usr/local/apache/php
COPY ./conf/tnsnames.ora /opt/oracle/product/12c/dbhome_1/network/admin
COPY ./src/test.php /usr/local/apache/htdocs
COPY ./src/test_oracle.php /usr/local/apache/htdocs

CMD ["tail","-f","/dev/null"]
