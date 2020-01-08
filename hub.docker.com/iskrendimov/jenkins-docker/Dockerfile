FROM jenkins:latest

USER root

RUN apt-get update && \
apt-get install -y wget php5 php5-xdebug jq && \
wget https://phar.phpunit.de/phpunit.phar && \
chmod +x phpunit.phar && \
mv phpunit.phar /usr/local/bin/phpunit


RUN ssh-keygen -t rsa -N "" -f /home/id_rsa

USER jenkins
