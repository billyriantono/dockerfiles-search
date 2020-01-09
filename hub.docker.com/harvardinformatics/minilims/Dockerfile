FROM centos:7

RUN yum -y install \
    httpd \
    php \
    php-mysql \
    php-cli \
    php-pdo \
    php-xml \
    mariadb \
    git

EXPOSE 80

RUN echo -e "ServerName ${HOSTNAME}\n" >> /etc/httpd/conf/httpd.conf && echo "ErrorLog /dev/stderr\n" >> /etc/httpd/conf/httpd.conf

WORKDIR /var/www/html

ARG MINILIMS_ROOT_DIR=amanitaBASE

ADD . $MINILIMS_ROOT_DIR

RUN mkdir -p $MINILIMS_ROOT_DIR/log && chown -R apache:apache $MINILIMS_ROOT_DIR

CMD ["/usr/sbin/httpd","-DFOREGROUND"]
