FROM ubuntu:16.04

MAINTAINER HoaDX "duongxuanhoa@gmail.com"

ENV LC_ALL=C.UTF-8

RUN apt-get update && apt-get install -y software-properties-common python-software-properties \
    && add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y software-properties-common wget git curl \
    && curl -sL https://deb.nodesource.com/setup_5.x | bash - \
    && apt-get update \
    && apt-get install -y --allow-unauthenticated graphviz phpunit nodejs \
       php7.1-cli php7.1-dev php7.1-curl php7.1-gd php7.1-gmp php7.1-json php7.1-ldap php7.1-mysql php7.1-odbc php7.1-pgsql php7.1-pspell php7.1-readline php7.1-recode php7.1-sqlite3 php7.1-tidy php7.1-xml php7.1-xmlrpc php7.1-bcmath php7.1-bz2 php7.1-enchant php7.1-imap php7.1-interbase php7.1-intl php7.1-mbstring php7.1-mcrypt php7.1-soap php7.1-sybase php7.1-xsl php7.1-zip php-memcache php-memcached php-pear \
        openjdk-8-jre libxext-dev libxrender-dev libxtst-dev \
    && pecl install xdebug \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/*

RUN useradd -m -u 5353 www \
    && mkdir /home/www/.PhpStorm2017.2 \
    && touch /home/www/.PhpStorm2017.2/.keep \
    && chown -R www:www /home/www \
    && mkdir /opt/phpstorm \
    && wget -O - https://download.jetbrains.com/webide/PhpStorm-2017.2.4.tar.gz | tar xzf - --strip-components=1 -C "/opt/phpstorm"

RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin

RUN phpenmod curl gd gmp json ldap mysql odbc pgsql pspell readline recode snmp sqlite3 tidy xml xmlrpc bcmath bz2 enchant imap interbase intl mbstring mcrypt soap sybase xsl zip xdebug memcache memcached

RUN wget -c http://static.phpmd.org/php/latest/phpmd.phar -O /usr/bin/phpmd.phar && chmod +x /usr/bin/phpmd.phar

RUN pear install PHP_CodeSniffer

RUN npm install -g bower

USER www

VOLUME /home/www/.PhpStorm2017.2

CMD ["/opt/phpstorm/bin/phpstorm.sh"]
