FROM centos:7
LABEL maintainer="zeno.zaplaic@abdn.ac.uk"

ENV REFRESHED_AT 2019-12-05
ENV PUBLIC_ROOT html
ENV SERVER_NAME localhost
ENV HOST_PORT_XDEBUG 9000

ADD ./oracle-instantclient18.3-basic-18.3.0.0.0-1.x86_64.rpm /tmp/oracle-instantclient18.3-basic-18.3.0.0.0-1.x86_64.rpm
ADD ./oracle-instantclient18.3-devel-18.3.0.0.0-1.x86_64.rpm /tmp/oracle-instantclient18.3-devel-18.3.0.0.0-1.x86_64.rpm

RUN yum install -y /tmp/oracle-instantclient18.3-basic-18.3.0.0.0-1.x86_64.rpm
RUN yum install -y /tmp/oracle-instantclient18.3-devel-18.3.0.0.0-1.x86_64.rpm

ENV LD_LIBRARY_PATH=/usr/lib/oracle/18.3/client64/lib/
ENV LD_LIBRARY_PATH64=/usr/lib/oracle/18.3/client64/lib/
ENV ORACLE_HOME=/usr/lib/oracle/18.3/client64/lib/

RUN yum update -y
RUN yum install httpd mod_ssl wget epel-release zip unzip nano -y
# Add IUS repository
RUN yum install \
        https://repo.ius.io/ius-release-el7.rpm \
        https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm -y
RUN yum install yum-utils 
RUN yum-config-manager --enable ius-testing
RUN yum update -y
# php and extensions
RUN yum install pear1 \
                php73-common \
                php73-bcmath \
                php73-devel \
                php73-gd \
                php73-imap \
                php73-ldap \
                php73-mbstring \
                php73-mysqlnd \
                php73-opcache \
                php73-pgsql \
                php73-pecl-imagick \
                php73-pecl-redis \
                php73-pecl-xdebug \
                php73-pdo \
                php73-soap \
                mod_php73 -y
# Install OCI8
RUN  echo "instantclient,/usr/lib/oracle/18.3/client64/lib" | pecl install oci8
# Add the Oracle instaclient library to apache
RUN echo 'LD_LIBRARY_PATH=/usr/lib/oracle/18.3/client64/lib' >> /etc/sysconfig/httpd

# Create location for the fpm socket
RUN mkdir -p /var/run/php-fpm 

# Create HTTPS certs
RUN openssl genrsa -out ca.key 2048
RUN openssl req -new -nodes -subj "/C=UK/ST=Aberdeenshire/L=Aberdeen/O=AccApps/CN=abdn.ac.uk" -key ca.key -out ca.csr
RUN openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt
RUN cp ca.crt /etc/pki/tls/certs
RUN cp ca.key /etc/pki/tls/private/ca.key
RUN cp ca.csr /etc/pki/tls/private/ca.csr
RUN sed -i 's/SSLCertificateFile \/etc\/pki\/tls\/certs\/localhost.crt/SSLCertificateFile \/etc\/pki\/tls\/certs\/ca.crt/g' /etc/httpd/conf.d/ssl.conf
RUN sed -i 's/SSLCertificateKeyFile \/etc\/pki\/tls\/private\/localhost.key/SSLCertificateKeyFile \/etc\/pki\/tls\/private\/ca.key/g' /etc/httpd/conf.d/ssl.conf

COPY ./.bashrc /root/
# Apache and PHP configs
COPY ./php/php.ini /etc/
COPY ./httpd/conf/httpd.conf /etc/httpd/conf/
COPY ./php.d/99-oci8.ini /etc/php.d/

EXPOSE 80
EXPOSE 443
EXPOSE 1521

# Install Supervisor for managing processes
RUN yum install -y python-setuptools
RUN easy_install supervisor==3.4.0
COPY ./supervisord/supervisord.conf /usr/etc/supervisord.conf

CMD ["/usr/bin/supervisord"]