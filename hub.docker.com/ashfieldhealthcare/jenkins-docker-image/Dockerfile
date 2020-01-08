FROM jenkins/jenkins:2.89.3
USER root
RUN apt-get update
RUN apt-get install -y \
 php-fpm \
 php-cli \
 php-curl \
 php-mbstring \
 php-mcrypt \
 php-mysql \
 php-json \
 php-xml \
 php-zip \
 php-all-dev \
 phpunit \
 phpunit-code-unit-reverse-lookup \
 phpunit-comparator \
 phpunit-dbunit \
 phpunit-global-state \
 phpunit-mock-object \
 phpunit-object-enumerator \
 phpunit-resource-operations \
 wget \
 curl \
 nano \
 composer \
 less 

USER jenkins
 
EXPOSE 8080
EXPOSE 50000
