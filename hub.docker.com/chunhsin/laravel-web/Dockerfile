FROM chunhsin/php-5.6

# Add remi repo
RUN yum -y install mysql55w
RUN yum -y install php56w-mysql

RUN composer global require "laravel/installer=~1.1"
ENV PATH=$PATH:/root/.composer/vendor/bin
