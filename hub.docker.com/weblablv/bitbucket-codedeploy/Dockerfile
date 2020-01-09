FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "nameserver 8.8.8.8" | tee /etc/resolv.conf > /dev/null

RUN apt-get update --fix-missing
RUN apt-get upgrade -y
RUN apt-get install -y python3
RUN apt-get install -y python-pip
RUN apt-get install -y zip
RUN apt-get install -y wget
RUN apt-get install -y php-cli
RUN apt-get install -y awscli
RUN apt-get install -y curl

RUN wget -O phpunit https://phar.phpunit.de/phpunit-6.5.phar && chmod +x phpunit && mv phpunit /usr/local/bin/phpunit
RUN pip install --upgrade pip
RUN pip install boto3==1.3.0

RUN ln -fs /usr/share/zoneinfo/UTC /etc/localtime
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN mkdir /opt/weblablv
ADD src /opt/weblablv
