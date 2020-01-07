FROM debian:stretch

RUN apt-get update && apt-get -y upgrade
RUN apt install -y apt-transport-https lsb-release ca-certificates
RUN apt install -y wget
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
RUN apt update
RUN apt install -y apache2
RUN apt install -y php7.2 php7.2-common php7.2-cli php7.2-fpm
RUN apt-get install -y libapache2-mod-php7.2
EXPOSE 80
EXPOSE 443

CMD apachectl -D FOREGROUND