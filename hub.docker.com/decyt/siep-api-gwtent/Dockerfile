FROM decaf/docker-api

# run as root
USER root

RUN apt-get install -y \
	alien \
	libaio-dev

ADD oracle/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm /tmp/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm
ADD oracle/oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm /tmp/oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm
ADD oracle/oracle-instantclient12.2-sqlplus-12.2.0.1.0-1.x86_64.rpm /tmp/oracle-instantclient12.2-sqlplus-12.2.0.1.0-1.x86_64.rpm

RUN alien -i /tmp/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm
RUN alien -i /tmp/oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm
RUN alien -i /tmp/oracle-instantclient12.2-sqlplus-12.2.0.1.0-1.x86_64.rpm

RUN rm /tmp/*.rpm

RUN echo 'export LD_LIBRARY_PATH="/usr/lib/oracle/12.2/client64/lib"' >> /root/.bashrc

RUN echo 'instantclient,/usr/lib/oracle/12.2/client64/lib' | pecl install oci8

ADD php/oci8.ini /usr/local/etc/php/conf.d/oci8.ini

RUN echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf && \
	ldconfig

# switch back
USER www-data