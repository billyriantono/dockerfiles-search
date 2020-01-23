
FROM tutum/lamp:latest
MAINTAINER chxj1992 chxj1992@gmail.com

#update apt sources list
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY sources.list /etc/apt/
RUN apt-get update

#composer
RUN apt-get install -qqy curl
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=bin --filename=composer

#nodejs
RUN curl -sL https://deb.nodesource.com/setup_0.12 | sudo bash -
RUN apt-get install -qqy nodejs


EXPOSE 80 3306

CMD ["/run.sh"]


