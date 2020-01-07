FROM debian:jessie

MAINTAINER Denis Lamard <lamard.denis@gmail.com>

RUN apt-get update 
RUN apt-get upgrade -y

RUN apt-get install -y python3 postgresql-client apt-utils python3-psycopg2 python3-pip supervisor

RUN pip3 install --upgrade pip

RUN pip3 install django

RUN pip3 install uwsgi

COPY uwsgi.ini /home/application/ 
COPY webapp /home/application/ 
COPY applications.conf /etc/supervisor/conf.d/

EXPOSE 8000

CMD ["/usr/bin/supervisord", "-n"]



