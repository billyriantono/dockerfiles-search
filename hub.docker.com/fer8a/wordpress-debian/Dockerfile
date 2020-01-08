FROM debian:jessie

RUN \

    apt-get update -y && \
    apt -y install wget curl ca-certificates apt-transport-https && \
    wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add - && \
    echo "deb https://packages.sury.org/php/ jessie main" | tee /etc/apt/sources.list.d/php.list && \
    apt-get update -y && \
    apt-get install -y apache2 php php-mysql libapache2-mod-php && \
    rm -rf /var/lib/apt/lists && \
    rm -rf /etc/apt/sources.list.d && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log && \
    rm /etc/apache2/sites-enabled/000-default.conf && \
    rm /etc/apache2/sites-available/000-default.conf && \
    rm /var/www/html/index.html && \
    cd /tmp && \
    curl -O https://wordpress.org/latest.tar.gz && \ 
    tar xzvf latest.tar.gz && \ 
    rm latest.tar.gz && \
    cp -r wordpress/* /var/www/html/ && \
    chown -R www-data:www-data /var/www/html/ && \ 
    chmod -R 755 /var/www/html/ 

EXPOSE 80

ENTRYPOINT ["/usr/sbin/apache2ctl"]

CMD ["-D", "FOREGROUND"]
