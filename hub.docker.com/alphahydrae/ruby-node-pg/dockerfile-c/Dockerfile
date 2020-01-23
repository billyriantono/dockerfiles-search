
FROM ubuntu:14.04

MAINTAINER Alexandre Cote

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y install nginx  sed python-pip python-dev uwsgi-plugin-python supervisor
RUN apt-get -y install python-dev libxml2-dev libxslt1-dev libffi-dev postgresql-server-dev-9.3
RUN apt-get -y install curl
RUN mkdir -p /var/log/nginx/app
RUN mkdir -p /var/log/uwsgi/app/

RUN curl -sL https://deb.nodesource.com/setup_5.x | sudo -E bash -
RUN apt-get -y install nodejs

RUN rm /etc/nginx/sites-enabled/default
COPY flask.conf /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/flask.conf /etc/nginx/sites-enabled/flask.conf
COPY uwsgi.ini /var/www/app/
RUN echo "daemon off;" >> /etc/nginx/nginx.conf


RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

copy app /var/www/app
RUN pip install -r /var/www/app/requirements.txt

EXPOSE 80
EXPOSE 8000
EXPOSE 2992

VOLUME /app

CMD ["/usr/bin/supervisord"]
