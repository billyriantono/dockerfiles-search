FROM centos:7
MAINTAINER Zeno Zaplaic "zeno.zaplaic@abdn.ac.uk"
ENV REFRESHED_AT 2018-11-13

ADD ./oracle-instantclient18.3-basic-18.3.0.0.0-1.x86_64.rpm /tmp/oracle-instantclient18.3-basic-18.3.0.0.0-1.x86_64.rpm
ADD ./oracle-instantclient18.3-devel-18.3.0.0.0-1.x86_64.rpm /tmp/oracle-instantclient18.3-devel-18.3.0.0.0-1.x86_64.rpm

RUN yum install -y /tmp/oracle-instantclient18.3-basic-18.3.0.0.0-1.x86_64.rpm
RUN yum install -y /tmp/oracle-instantclient18.3-devel-18.3.0.0.0-1.x86_64.rpm

ENV LD_LIBRARY_PATH=/usr/lib/oracle/18.3/client64/lib/
ENV LD_LIBRARY_PATH64=/usr/lib/oracle/18.3/client64/lib/
ENV ORACLE_HOME=/usr/lib/oracle/18.3/client64/lib/

RUN yum update -y
RUN yum install zip unzip -y
RUN yum install httpd mod_ssl wget epel-release -yq
RUN yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm -y
RUN yum install yum-utils #needed by yum-config-manager
RUN yum-config-manager --enable remi-php71
RUN yum update -y
RUN yum install php \
                php-mysqlnd \
                php-bcmath \
                php-xml \
                php-gd \
                php-imap \
                php-ldap \
                php-mbstring \
                php-mcrypt \
                php-mssql \
                php-pdo \
                php-opcache \
                php-soap \
                php-devel \
                gcc \
                gcc-c++ \
                autoconf \
                automake \
                php-pear \
                php-redis \
                php-zip \
                php-oci8 -y
RUN pecl install Xdebug

# Add the oracle library to apache
RUN echo 'LD_LIBRARY_PATH=/usr/lib/oracle/18.3/client64/lib' >> /etc/sysconfig/httpd

ENV PUBLIC_ROOT html
ENV SERVER_NAME localhost
# Make the server name configurable
RUN sed -i 's!#ServerName www.example.com!ServerName ${SERVER_NAME}!g' /etc/httpd/conf/httpd.conf
# Make the webroot configurable
RUN sed -i 's!/var/www/html!/var/www/${PUBLIC_ROOT}!g' /etc/httpd/conf/httpd.conf
# Turn off EnableSendFile in httpd.conf
RUN sed -i 's/EnableSendfile on/EnableSendfile off/g' /etc/httpd/conf/httpd.conf
# Allow the .htaccess file to override Apache settings
RUN sed -i 's/AllowOverride None/AllowOverride All/g' /etc/httpd/conf/httpd.conf

# Create HTTPS certs
RUN openssl genrsa -out ca.key 2048
RUN openssl req -new -nodes -subj "/C=UK/ST=Aberdeenshire/L=Aberdeen/O=AccApps/CN=abdn.ac.uk" -key ca.key -out ca.csr
RUN openssl x509 -req -days 365 -in ca.csr -signkey ca.key -out ca.crt
RUN cp ca.crt /etc/pki/tls/certs
RUN cp ca.key /etc/pki/tls/private/ca.key
RUN cp ca.csr /etc/pki/tls/private/ca.csr
RUN sed -i 's/SSLCertificateFile \/etc\/pki\/tls\/certs\/localhost.crt/SSLCertificateFile \/etc\/pki\/tls\/certs\/ca.crt/g' /etc/httpd/conf.d/ssl.conf
RUN sed -i 's/SSLCertificateKeyFile \/etc\/pki\/tls\/private\/localhost.key/SSLCertificateKeyFile \/etc\/pki\/tls\/private\/ca.key/g' /etc/httpd/conf.d/ssl.conf


# Copy the php ini file
COPY ./php.ini /etc/

EXPOSE 80
EXPOSE 443
EXPOSE 1521

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

# Add Oracle library to path inside Docker machine (this means that OCI8 will
# now work on the command line, which lets you use Laravel's `php artisan`).
RUN echo 'export LD_LIBRARY_PATH=/usr/lib/oracle/18.3/client64/lib' >> /root/.bashrc
# Browse to the webroot by default 
RUN echo 'cd /var/www' >> /root/.bashrc

CMD ["/run-httpd.sh"]
