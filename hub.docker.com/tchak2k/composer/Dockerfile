FROM php:5.6-cli


RUN \
    apt-get update

#RUN apt-get install -y php-xml
#RUN apt-get install -y composer
RUN  apt-get install -y curl
RUN apt-get install -y sudo
# initializing user env
# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer



    RUN mkdir /app && chown 1000:1000 /app

#RUN apt-get install -y php5-mysql


RUN docker-php-ext-configure mysqli
RUN docker-php-ext-install mysqli
RUN docker-php-ext-configure mysql
RUN docker-php-ext-install mysql

RUN docker-php-ext-configure pdo
RUN docker-php-ext-install pdo

RUN docker-php-ext-configure pdo_mysql
RUN docker-php-ext-install pdo_mysql

RUN apt-get install -y git
RUN apt-get install -y zip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#USER developer
#ENV HOME /home/developer




WORKDIR /app
#RUN composer update

ENTRYPOINT ["composer"]
