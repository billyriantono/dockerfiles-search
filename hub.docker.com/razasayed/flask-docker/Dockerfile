FROM ubuntu:14.04
MAINTAINER Raza Sayed <raza.sayed@gmail.com>

RUN apt-get update
RUN apt-get -y install nginx
RUN apt-get -y install supervisor
RUN apt-get -y install python3-pip
RUN pip3 install uwsgi flask

ADD ./app /app
ADD ./config /config

RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN rm /etc/nginx/sites-enabled/default

RUN ln -s /config/nginx.conf /etc/nginx/sites-enabled/
RUN ln -s /config/supervisor.conf /etc/supervisor/conf.d/

EXPOSE 80
CMD ["supervisord", "-n"]

