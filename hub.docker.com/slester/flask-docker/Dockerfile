FROM ubuntu:14.10
MAINTAINER Real Python <info@realpythong.com>

# dependencies
RUN apt-get update
RUN apt-get install -y nginx supervisor python3-pip
RUN pip3 install uwsgi flask

ADD ./app /app
ADD ./config /config

# setup config
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN rm /etc/nginx/sites-enabled/default

RUN ln -s /config/nginx.conf /etc/nginx/sites-enabled/
RUN ln -s /config/supervisor.conf /etc/supervisor/conf.d/

EXPOSE 80
CMD ["supervisord", "-n"]
