FROM ubuntu:bionic
MAINTAINER luismesalas

RUN apt-get update
RUN apt-get install -y tzdata
RUN ln -fs /usr/share/zoneinfo/Europe/Madrid /etc/localtime
RUN dpkg-reconfigure --frontend noninteractive tzdata
RUN apt-get install -y php7.2 php7.2-common php7.2-gd php7.2-mysql php7.2-sqlite3 php7.2-mbstring php7.2-json php7.2-xml php7.2-curl php7.2-cli sqlite3 git nodejs npm
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN git clone https://github.com/contentacms/contenta_jsonapi.git; cd contenta_jsonapi; sh scripts/development/build-contenta_jsonapi.sh

EXPOSE 8888

ENTRYPOINT contenta_jsonapi/scripts/development/build-contenta_jsonapi.sh
