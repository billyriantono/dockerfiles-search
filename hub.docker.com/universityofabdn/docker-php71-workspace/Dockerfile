FROM universityofabdn/docker-php71:latest

MAINTAINER Zeno Zaplaic <zeno.zaplaic@abdn.ac.uk>

RUN yum install epel-release -y
RUN yum install git nano -y

# Add nodejs repository
RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash -
# Install nodejs and npm
RUN yum install nodejs -y
# Install gulp globally
RUN npm install gulp bower vue-cli -g -y

# Install Composer
RUN wget https://getcomposer.org/installer && php installer && php composer.phar && mv composer.phar /usr/local/bin/composer
ENV COMPOSER_HOME=/usr/local/composer
ENV PATH=/usr/local/composer/vendor/bin/:${PATH}

# Install PHP Code Sniffer
RUN composer global require "squizlabs/php_codesniffer=*"
# Install PHPUnit
RUN composer global require "phpunit/phpunit=*"

# Install php-ast, required for phan
RUN yum install php-ast -y

# Install phan
RUN git clone https://github.com/phan/phan.git \
    && cd phan \
    && composer install \
    && ./test \
    && chmod a+x phan \
    && ln -s /phan/phan /usr/local/bin/phan
