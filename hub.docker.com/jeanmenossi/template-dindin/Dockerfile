FROM wyveo/nginx-php-fpm:latest
LABEL maintainer="Nnatho Technologies - 2019"
LABEL description="DinDin dev template with PHP 7.3 and Lumen v0.3"

RUN apt-get update
RUN apt-get install -y doxygen
RUN apt-get install -y graphviz
RUN apt-get install -y vim



COPY default.conf /etc/nginx/conf.d/
COPY doxygen.conf /etc/nginx/conf.d/

COPY gendoc /bin
RUN chmod +x /bin/gendoc 

RUN mkdir -p /home/user/doc
RUN chmod -R 777 /home/user/doc
COPY doxygen-configuration-file.conf /home/user
COPY dindinlogo.png /home/user


#WORKDIR /home/user/doc
#RUN doxygen doxygen-configuration-file.conf

COPY rc.local /etc/
RUN chmod +x /etc/rc.local


RUN composer global require "laravel/lumen-installer"
RUN composer global require "firebase/php-jwt"
RUN composer global require "guzzlehttp/guzzle"



WORKDIR /usr/share/nginx/
RUN rm -rf html/
RUN ln -s /home/user/doc/html doxygen-generated-files



#RUN composer create-project --prefer-dist laravel/lumen blog
RUN mkdir -p api-wallet/public
RUN ln -s /home/user/api_wallet/src/api_wallet/public html
WORKDIR /home/user/api_wallet/src/api_wallet/