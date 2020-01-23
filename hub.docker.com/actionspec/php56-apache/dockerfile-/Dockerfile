FROM ubuntu


MAINTAINER Adam Copley version: 0.1

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y software-properties-common
RUN apt-get install -y  python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php 
RUN apt-get update
RUN apt-get install -y php7.2
RUN apt-get install -y  php-pear php7.2-curl php7.2-dev php7.2-gd php7.2-mbstring php7.2-zip php7.2-mysql php7.2-xml
RUN update-alternatives --set php /usr/bin/php7.2

RUN apt-get install -y git
RUN apt-get install -y nodejs npm

RUN apt-get update
RUN apt-get install build-essential chrpath libssl-dev libxft-dev -y
RUN apt-get install libfreetype6 libfreetype6-dev -y
RUN apt-get install libfontconfig1 libfontconfig1-dev -y
RUN cd ~
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN tar xvjf phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN mv phantomjs-2.1.1-linux-x86_64 /usr/local/share
RUN ln -sf /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin

RUN apt-get install -y curl
RUN chmod 0777 /usr/local/bin
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
