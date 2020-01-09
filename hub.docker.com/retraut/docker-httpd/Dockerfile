FROM retraut/docker-centos6.8-base
MAINTAINER retraut@gmail.com

RUN yum -y install http://rpms.famillecollet.com/enterprise/remi-release-6.rpm && \
    yum -y install httpd && \
    yum -y install --enablerepo=remi,remi-php56 php php-devel php-mcrypt  php-pecl-xdebug php-pecl-xhprof php-twig-ctwig php-pecl-imagick php-tcpdf php-pecl-zip php-pecl-jsonc-devel php-pear php-soap php-cli php-symfony-common php-odbc php-xml php-gmp php-gd php php-tidy php-magickwand php-common php-mysqlnd php-process php-phpseclib php-opcache php-pecl-rar php-symfony-class-loader php-tcpdf-dejavu-sans-fonts php-pecl-jsonc php-pdo php-pdo php-mbstring php-pecl-apcu php-php-gettext php-bcmath && \
    yum -y clean all && \
    rm -fr /var/cache && \
    chown -R dev:www /var/www/ && \
    curl https://getcomposer.org/composer.phar > /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer
    
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
EXPOSE 80
