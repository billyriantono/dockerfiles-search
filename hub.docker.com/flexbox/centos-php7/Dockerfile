FROM centos:latest

LABEL name="Flexbox CentOS 7.4 + PHP 7.1 Image" \
    maintainer="Alex Karshin <https://flexbox.it>" \
    license="GPLv3" \
    build-date="20171114" \
    source="https://bitbucket.org/flexboxIT/centos-php7"

# update yum
RUN yum clean all; yum -y update --nogpgcheck
RUN yum -y install yum-utils

RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm; \
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

# Install some must-haves
RUN yum -y install --nogpgcheck \\
    epel-release \
    wget \
    git \
    nano \
    postfix \
    gcc-c++ \
    make

RUN yum -y install \
    php71w \
    php71w-bcmath \
    php71w-cli \
    php71w-curl \
    php71w-devel \
    php71w-gd \
    php71w-fpm \
    php71w-imagick \
    php71w-intl \
    php71w-mbstring \
    php71w-mcrypt \
    php71w-mysqlnd \
    php71w-opcache --nogpgcheck \
    php71w-pdo \
    php71w-xml \
    php71w-zip

RUN curl https://phar.phpunit.de/phpunit.phar -L -o phpunit.phar && \
    chmod +x phpunit.phar && \
    mv phpunit.phar /usr/local/bin/phpunit

RUN rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
RUN yum -y install nginx --nogpgcheck

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt. Maybe a new version was released and you forgot to update the verification hash?'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash - && \
    yum -y install nodejs

RUN wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo && \
    yum -y install yarn

RUN mkdir -p /tmp
RUN chown -R nginx:nginx /var/lib/php/session && chmod 0777 /var/lib/php/session

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
