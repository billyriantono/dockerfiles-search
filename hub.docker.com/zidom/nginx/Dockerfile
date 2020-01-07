FROM ubuntu:14.04
MAINTAINER Mohammad Zolfaghari <zidom72@gmail.com>

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update -y
RUN apt-get install -y software-properties-common

RUN add-apt-repository -y ppa:nginx/stable
RUN apt-get update
RUN apt-get -y install nginx

ADD default.tmpl /etc/nginx/sites-available/default.tmpl

ADD start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

WORKDIR /var/www

VOLUME ["/var/www"]
EXPOSE 80

CMD ["start-container"]
