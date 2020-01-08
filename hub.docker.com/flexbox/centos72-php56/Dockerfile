FROM centos:7.2.1511

LABEL name="Flexbox CentOS 7.2.1511 + PHP 5.6 Image" \
    maintainer="Alex Karshin <https://flexbox.it>" \
    license="GPLv3" \
    build-date="20171003" \
    source="https://bitbucket.org/flexboxIT/centos72-php56"

RUN yum clean all; yum -y update --nogpgcheck
RUN yum -y install yum-utils; \
    yum clean all; \
    rm -rf /var/cache/yum

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm; \
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

RUN yum clean all; \
    yum -y install --nogpgcheck \
    epel-release \
    git \
    nano \
    postfix \
    gcc-c++ \
    make; \
    yum clean all; \
    rm -rf /var/cache/yum

RUN yum -y install \
    php56w \
    php56w-bcmath \
    php56w-cli \
    php56w-curl \
    php56w-devel \
    php56w-gd \
    php56w-fpm \
    php56w-imagick \
    php56w-intl \
    php56w-mbstring \
    php56w-mcrypt \
    php56w-mysqlnd \
    php56w-opcache --nogpgcheck \
    php56w-pdo \
    php56w-xml \
    php56w-zip; \
    yum clean all; \
    rm -rf /var/cache/yum

RUN rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm; \
    yum -y install nginx --nogpgcheck; \
    yum clean all; \
    rm -rf /var/cache/yum

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt. Maybe a new version was released and you forgot to update the verification hash?'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

RUN mkdir -p /tmp; \
    chown -R nginx:nginx /var/lib/php/session && chmod 0777 /var/lib/php/session

COPY start.sh /tmp/start.sh
COPY php/memory.ini /etc/php.d/01-memory.ini
COPY php/datetime.ini /etc/php.d/01-datetime.ini
COPY php/session.ini /etc/php.d/01-session.ini
COPY php/www.conf /etc/php-fpm.d/www.conf
COPY postfix/main.cf /etc/postfix/main.cf
COPY postfix/main.cf.working /etc/postfix/main.cf.working

WORKDIR "/html"

EXPOSE 80 443

RUN usermod -u 1000 nginx
RUN groupmod -g 1000 nginx

CMD ["/tmp/start.sh"]
