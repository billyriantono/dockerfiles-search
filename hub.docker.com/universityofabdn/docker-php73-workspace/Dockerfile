FROM universityofabdn/docker-php73:latest

LABEL maintainer="zeno.zaplaic@abdn.ac.uk"

RUN yum install gnupg2 git bzip2 zip unzip which -y

# Add nodejs repository
RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash -
# Install nodejs and npm
RUN yum install nodejs -y
# Install gulp and npm-check-updates globally
RUN npm install gulp npm-check-updates -g -y

# Disable Xdebug because it's slowing down Composer and static analysis tools
RUN mv /etc/php.d/15-xdebug.ini /etc/php.d/15-xdebug.disabled

# Install Composer
RUN wget https://getcomposer.org/installer && php installer && php composer.phar && mv composer.phar /usr/local/bin/composer
ENV COMPOSER_HOME=/usr/local/composer
ENV PATH=/usr/local/composer/vendor/bin/:${PATH}

# Install Phive (The Phar Installation and Verification Environment)
RUN wget -O phive.phar "https://phar.io/releases/phive.phar"
RUN wget -O phive.phar.asc "https://phar.io/releases/phive.phar.asc"
RUN gpg --keyserver hkps.pool.sks-keyservers.net --recv-keys 0x9D8A98B29B2D5D79
RUN gpg --verify phive.phar.asc phive.phar
RUN rm phive.phar.asc
RUN chmod +x phive.phar
RUN mv phive.phar /usr/local/bin/phive

# Install PHPUnit
RUN phive install --trust-gpg-keys phpunit

# Install PHP Code Sniffer
RUN composer global require "squizlabs/php_codesniffer"
RUN composer global require "dealerdirect/phpcodesniffer-composer-installer"
RUN composer global require "phpcompatibility/php-compatibility"
# Adds analysis of problematic variable use.
RUN composer global require "sirbrillig/phpcs-variable-analysis"

# No conflicts for your bin dependencies
RUN composer global require bamarni/composer-bin-plugin
#  Easiest way to start using PHP CS Fixer and PHP_CodeSniffer with 0-knowledge
RUN composer global bin "ecs" require "symplify/easy-coding-standard"
# Instant upgrades and instant refactoring of any PHP 5.3+ code
RUN composer global bin "rector" require "rector/rector:0.6.0"
# Laravel Envoy for running deployments
RUN composer global bin "envoy" require "laravel/envoy"
# Static analysis tool
RUN composer global bin "phpstan" require "phpstan/phpstan"
# Upload only the files that changed since the last upload
RUN curl https://raw.githubusercontent.com/git-ftp/git-ftp/master/git-ftp > /bin/git-ftp && chmod 755 /bin/git-ftp

# Install and enable php-ast, required for phan
RUN pecl install ast -y
COPY ./php.d/50-ast.ini /etc/php.d/

# Install phan
RUN git clone https://github.com/phan/phan.git \
    && cd phan \
    && composer install \
    # && ./test \ # phan is tested on php 7.1.22, some of the tests seem to fail on 7.3
    && chmod a+x phan \
    && ln -s /phan/phan /usr/local/bin/phan

# Make sure that all the packages are registered correctly
RUN composer global install

# Install and enable mcrypt - this is still needed for legacy Laravel 4.2 applications
# RUN yum install libmcrypt-devel
# RUN yes '' | pecl install -f mcrypt
# RUN echo "extension=mcrypt.so" > /etc/php.d/60-mcrypt.ini