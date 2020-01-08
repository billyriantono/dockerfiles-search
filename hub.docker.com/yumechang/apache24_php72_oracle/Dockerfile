FROM yumechang/apache24_php72

RUN apt update && apt upgrade -y && apt install -y unzip libaio-dev alien libaio1 wget &&\
    rm -rf /var/lib/apt/lists/

# Oracle instantclient
RUN cd /tmp/ &&\
    wget https://blog.hamibook.com.tw/wp-content/uploads/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm &&\
    wget https://blog.hamibook.com.tw/wp-content/uploads/oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm &&\
    alien -i oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm &&\
    alien -i oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm &&\
    rm -f *.rpm

RUN touch /etc/ld.so.conf.d/oracle.conf && echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle.conf && ldconfig

ENV ORACLE_HOME=/usr/lib/oracle/12.2/client64/
#RUN echo 'instantclient,/usr/lib/oracle/12.2/client64/lib' | pecl install oci8 && docker-php-ext-enable oci8 && rm -rf /tmp/pear/
RUN docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/lib/oracle/12.2/client64/lib,12.2 &&\
    docker-php-ext-install oci8 &&\
    docker-php-ext-configure pdo_oci --with-pdo-oci=instantclient,/usr/lib/oracle/12.2/client64/lib,12.2 &&\
    docker-php-ext-install pdo_oci &&\
    rm -rf /tmp/pear/
