# Used to build megaorbco/php-composer

FROM ubuntu:bionic

ENV HOME /root
ENV LC_ALL          C.UTF-8
ENV LANG            en_US.UTF-8
ENV LANGUAGE        en_US.UTF-8

RUN apt-get update
RUN apt-get install -y --no-install-recommends apt-utils

RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php  && \
	apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata

RUN apt-get install php7.2 -y


RUN apt-get install libxml2-dev -y
RUN apt-get install -y curl

RUN apt-get install -y unzip
RUN apt-get install -y php7.2-xml
RUN apt-get install -y php7.2-curl
RUN apt-get install -y php7.2-mongodb
RUN apt-get install -y php7.2-mbstring
RUN apt-get install -y php7.2-bcmath
RUN apt-get install -y php7.2-zip
RUN apt-get install -y php7.2-gd

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get install git -y

RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt install nodejs -y
RUN rm nodesource_setup.sh
