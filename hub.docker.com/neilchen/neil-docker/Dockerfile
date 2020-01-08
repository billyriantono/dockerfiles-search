FROM feifan/supervisord

MAINTAINER neilchen(neil.chen.nj@gmail.com)

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | sudo bash -
RUN apt-get install -y nodejs


RUN apt-get install -y python-setuptools python-software-properties software-properties-common
RUN easy_install pip
RUN sudo add-apt-repository -y ppa:nginx/stable
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
RUN apt-get install -y gcc make build-essential
RUN apt-get install -y nginx-full
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

ADD nginx.conf /etc/supervisor/conf.d/nginx.conf
RUN mkdir /var/www