# Version: 0.0.1

FROM python:3.5-slim

MAINTAINER Rafael Acorsi <rafaelacorsi@gmail.com>

RUN apt-get update && \
    apt-get autoremove && \
    apt-get autoclean && \
    apt-get -y install nginx-full && \
    apt-get -y install build-essential python-dev python-pip supervisor && \
    pip install --upgrade pip

RUN mkdir -p /var/log/nginx/app
RUN mkdir -p /var/log/uwsgi/app/

COPY gzip_static.conf /etc/nginx/conf.d/flask/gzip_static.conf
COPY gzip.conf /etc/nginx/conf.d/flask/gzip.conf
# COPY uwsgi-emperor.conf /etc/init/uwsgi-emperor.conf
COPY flask.conf /etc/nginx/sites-available/flask

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
# setup nginx
RUN ln -s /etc/nginx/sites-available/flask /etc/nginx/sites-enabled/flask && \
    rm /etc/nginx/sites-enabled/default

RUN mkdir -p /var/log/supervisor
COPY supervisor.conf /etc/supervisor/conf.d/

COPY app /var/www/app
RUN pip install -r /var/www/app/requirements.txt

CMD ["supervisord", "-n"]
