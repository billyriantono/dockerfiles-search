FROM tairoroberto/base:latest

MAINTAINER Tairo Roberto <tairoroberto@gmail.com>

COPY oracle-instantclient12.1-basic.deb /home/zanthus/oracle-instantclient12.1-basic.deb
COPY oracle-instantclient12.1-devel.deb /home/zanthus/oracle-instantclient12.1-devel.deb
COPY oracle-instantclient12.1-jdbc.deb /home/zanthus/oracle-instantclient12.1-jdbc.deb
COPY oracle-instantclient12.1-odbc.deb /home/zanthus/oracle-instantclient12.1-odbc.deb
COPY oracle-instantclient12.1-sqlplus.deb /home/zanthus/oracle-instantclient12.1-sqlplus.deb
COPY oracle-instantclient12.1-tools.deb /home/zanthus/oracle-instantclient12.1-tools.deb

COPY Zanthus_pdv.zip /home/zanthus/Zanthus_pdv.zip
COPY pdvJava.zip /home/zanthus/pdvJava.zip

RUN apt-get update -y
RUN apt-get install -y apt-utils
RUN apt-get install -y software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php

RUN apt-get update -y
RUN apt-get install -y unzip && \
    apt-get install -y apache2 && \
    apt-get install -y php5.6 && \
    apt-get install -y php5.6-dev && \
    apt-get install -y php5.6-cli &&  \
    apt-get install -y php5.6-common &&  \
    apt-get install -y php5.6-curl &&  \
    apt-get install -y php5.6-gd &&  \
    apt-get install -y php5.6-ldap &&  \
    apt-get install -y php5.6-sybase &&  \
    apt-get install -y php5.6-pgsql &&  \
    apt-get install -y php5.6-recode &&  \
    apt-get install -y php5.6-sqlite3 &&  \
    apt-get install -y php5.6-json &&  \
    apt-get install -y php5.6-bz2 &&  \
    apt-get install -y php5.6-mcrypt &&  \
    apt-get install -y php5.6-odbc &&  \
    apt-get install -y php-memcached &&  \
    apt-get install -y php5.6-readline &&  \
    apt-get install -y php5.6-xml &&  \
    apt-get install -y php5.6-dom &&  \
    apt-get install -y php5.6-xmlrpc &&  \
    apt-get install -y php5.6-xsl &&  \
    apt-get install -y php5.6-bcmath &&  \
    apt-get install -y php5.6-mbstring &&  \
    apt-get install -y php5.6-soap &&  \
    apt-get install -y php5.6-zip && \
    apt-get install -y libapache2-mod-php5.6 && \
    apt-get install -y libaio1 libaio-dev && \
    apt-get install -y nano && \
    apt-get install -y memcached && \
    apt-get install -y zlib1g-dev && \
    apt-get install -y libxrender1 && \
    apt-get install -y libxi6 && \
    apt-get install -y libxtst6 && \
    apt-get install -y x11-xserver-utils

RUN unzip /home/zanthus/Zanthus_pdv.zip -d /

RUN dpkg -i /home/zanthus/oracle-instantclient12.1-basic.deb && \
    dpkg -i /home/zanthus/oracle-instantclient12.1-devel.deb && \
    dpkg -i /home/zanthus/oracle-instantclient12.1-jdbc.deb && \
    dpkg -i /home/zanthus/oracle-instantclient12.1-odbc.deb && \
    dpkg -i /home/zanthus/oracle-instantclient12.1-sqlplus.deb && \
    dpkg -i /home/zanthus/oracle-instantclient12.1-tools.deb

RUN apt-get update -y && apt-get install -y wget

RUN mkdir -p /Zanthus/Zeus/lib && \
    cd /Zanthus/Zeus/lib && \
    wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/so/* && \
    wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/Terceiros/ZANSINC/Linux/lib/*

RUN mkdir -p /Zanthus/Zeus/lib_64 && \
    cd /Zanthus/Zeus/lib_64 && \
    wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/so_r64/*

RUN mkdir -p /Zanthus/Zeus/lib_co5 && \
    cd /Zanthus/Zeus/lib_co5 && \
    wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/so_co5/*

RUN mkdir -p /Zanthus/Zeus/lib_ubu && \
    cd /Zanthus/Zeus/lib_ubu && \
    wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/so_ubu/*


ENV KC_ZMAN_CZ_EXL "KC_ZMAN_1_X_118_381_CZ.EXL"
ENV KC_ZMAN_CZ_TARGZ "KC_ZMAN_1_X_118_381_CZ.tar.gz"

RUN mkdir -p /Zanthus/Zeus/lib_kernz && \
    cd /Zanthus/Zeus/lib_kernz && \
    wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/KernD/v2_1/*.so && \
    wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/_Complementares/kernz/2_4/*.so

RUN wget -c ftp://ftp.zanthus.com.br:2142/pub/Zeus_Frente_de_Loja/v_1_X_118/$KC_ZMAN_CZ_EXL
RUN mv $KC_ZMAN_CZ_EXL $KC_ZMAN_CZ_TARGZ
RUN tar -zxvf $KC_ZMAN_CZ_TARGZ
RUN rm -f -r $KC_ZMAN_CZ_TARGZ

RUN ln -s -f /lib/x86_64-linux-gnu/libcrypto.so.1.0.0 /lib/x86_64-linux-gnu/libcrypto.so.6
RUN ln -s -f /lib/x86_64-linux-gnu/libssl.so.1.0.0 /lib/x86_64-linux-gnu/libssl.so.6

## MENCHACHE PHP ###
RUN apt-get install -y php-memcache

## XDEBUG PHP ###
RUN echo "[XDebug]" >> /etc/php/5.6/apache2/php.ini && \
    echo "zend_extension=/Zanthus/Zeus/lib_kernz/xdebug.so" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.default_enable = 1" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.show_exception_trace = 1" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.show_local_vars = 1" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.var_display_max_data   = -1" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.max_nesting_level = 250" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.remote_enable = 1" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.remote_port = 9000" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.remote_autostart = 1" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.remote_handler=dbgp" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.remote_connect_back = 1" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.idekey=\"PHPSTORM\"" >> /etc/php/5.6/apache2/php.ini && \
    echo "xdebug.remote_host=127.0.0.1" >> /etc/php/5.6/apache2/php.ini && \
    echo "\n" >> /etc/php/5.6/apache2/php.ini

RUN echo "[XDebug]" >> /etc/php/5.6/cli/php.ini && \
    echo "zend_extension=/Zanthus/Zeus/lib_kernz/xdebug.so" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.default_enable = 1" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.show_exception_trace = 1" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.show_local_vars = 1" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.var_display_max_data   = -1" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.max_nesting_level = 250" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.remote_enable = 1" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.remote_port = 9000" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.remote_autostart = 1" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.remote_handler=dbgp" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.remote_connect_back = 1" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.idekey=\"PHPSTORM\"" >> /etc/php/5.6/cli/php.ini && \
    echo "xdebug.remote_host=127.0.0.1" >> /etc/php/5.6/cli/php.ini && \
    echo "\n" >> /etc/php/5.6/cli/php.ini

### SET TIME ZONE AND CHARSET TO PHP ###
RUN echo "date.timezone = America/Sao_Paulo" >> /etc/php/5.6/apache2/php.ini && \
    echo "\n" >> /etc/php/5.6/apache2/php.ini && \
    echo "default_charset = \"ISO-8859-1\"" >> /etc/php/5.6/apache2/php.ini && \
    echo "\n" >> /etc/php/5.6/apache2/php.ini

RUN #Configura Timezone e charset
RUN echo "date.timezone = America/Sao_Paulo" >> /etc/php/5.6/cli/php.ini && \
    echo "\n" >> /etc/php/5.6/cli/php.ini && \
    echo "default_charset = \"ISO-8859-1\"" >> /etc/php/5.6/cli/php.ini && \
    echo "\n" >> /etc/php/5.6/cli/php.ini

### SET ZEND LOADER TO PHP ###
RUN echo "zend_extension=/Zanthus/Zeus/lib_kernz/ZendGuardLoader.so" >> /etc/php/5.6/apache2/php.ini && \
    echo "zend_extension=/Zanthus/Zeus/lib_kernz/ZendGuardLoader.so" >> /etc/php/5.6/cli/php.ini

### SET OPCACHE TO PHP ####
RUN echo "zend_extension=/Zanthus/Zeus/lib_kernz/opcache.so" >> /etc/php/5.6/apache2/php.ini && \
    echo "zend_extension=/Zanthus/Zeus/lib_kernz/opcache.so" >> /etc/php/5.6/cli/php.ini

### SET KERNZ TO PHP ####
RUN echo "extension=/Zanthus/Zeus/lib_kernz/kernz.so" >> /etc/php/5.6/apache2/php.ini && \
    echo "extension=/Zanthus/Zeus/lib_kernz/kernz.so" >> /etc/php/5.6/cli/php.ini

### SET OCI TO PHP ####
RUN echo "extension=/Zanthus/Zeus/lib_kernz/oci8.so" >> /etc/php/5.6/apache2/php.ini && \
    echo "extension=/Zanthus/Zeus/lib_kernz/oci8.so" >> /etc/php/5.6/cli/php.ini

### SET MENCACHED TO PHP SAAS ####
#RUN echo "session.save_handler = memcache" >> /etc/php/5.6/apache2/php.ini
#RUN echo "session.save_path = \"tcp://127.0.0.1:11211?timeout=5\"" >> /etc/php/5.6/apache2/php.ini
#RUN echo "session.save_handler = memcache" >> /etc/php/5.6/cli/php.ini
#RUN echo "session.save_path = \"tcp://127.0.0.1:11211?timeout=5\"" >> /etc/php/5.6/cli/php.ini

### SET REWRITE MODE APACHE ###
RUN a2enmod  rewrite

RUN echo "\n" >> /etc/ld.so.conf && \
    echo "/Zanthus/Zeus" >> /etc/ld.so.conf && \
    echo "/Zanthus/Zeus/lib" >> /etc/ld.so.conf && \
    echo "/Zanthus/Zeus/lib_64" >> /etc/ld.so.conf && \
    echo "/Zanthus/Zeus/lib_kernz" >> /etc/ld.so.conf && \
    echo "/Zanthus/Zeus/lib_co5" >> /etc/ld.so.conf && \
    echo "/Zanthus/Zeus/lib_ubu" >> /etc/ld.so.conf && \
    ldconfig

RUN apt-get upgrade -y

RUN apt-get clean -y && apt-get autoclean -y && apt-get autoremove -y  && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Seta variável de desenvolvimento na pasta /tmp
RUN touch /tmp/__desenvolv.zan

RUN rm -rf /home/zanthus/*

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

ADD 000-default.conf /etc/apache2/sites-enabled/000-default.conf

RUN rm -rf /etc/apache2/apache2.conf
ADD apache2.conf /etc/apache2/apache2.conf

RUN rm -rf /var/www/*

COPY index.php /var/www/index.php

WORKDIR /var/www/

EXPOSE 80

EXPOSE 9000

VOLUME /var/www/

VOLUME /var/log/apache2

VOLUME /Zanthus/Zeus/Manager

ONBUILD RUN chmod -R 777 /var/www

CMD /usr/sbin/apache2ctl -D FOREGROUND
