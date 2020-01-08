FROM ubuntu:16.04

VOLUME [ "/keys" ]

WORKDIR /jenkins

ENV TIMEZONE="Europe/Paris"
RUN apt-get update
RUN apt-get install -y wget tzdata inetutils-ping

RUN echo $TIMEZONE > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update

RUN wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war

RUN apt-get install software-properties-common -y
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update && apt-get install -y php5.6 php5.6-mbstring php5.6-mcrypt php5.6-mysql php5.6-xml php5.6-soap
RUN wget https://getcomposer.org/composer.phar && mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

RUN apt-get install -y python-pip && pip install fabric==1.14.0

EXPOSE 8080

RUN LC_ALL=C.UTF-8 add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update && apt-get install -y openjdk-8-jre

RUN apt-get install -y git
RUN apt-get install -y zip unzip php5.6-zip php5.6-curl curl
RUN apt-get install -y php7.2-cli php7.2-curl php7.2-zip php7.2-dom php7.2-xml php7.2-mysql && update-alternatives --set php /usr/bin/php7.2

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y build-essential nodejs

RUN apt-get install -y traceroute
RUN apt-get install -y vim

CMD /usr/bin/java -jar /jenkins/jenkins.war
