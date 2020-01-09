# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.
FROM phusion/baseimage:latest

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# ...put your own build instructions here...
RUN apt-get update; apt-get upgrade -y
RUN apt-get install -y nginx-extras rabbitmq-server python3-pip python3-dev build-essential


ADD requirements.txt manage.py /app/
ADD gmailpurge /app/gmailpurge/
ADD purger /app/purger/
ADD conf/nginx /etc/nginx

WORKDIR /app
RUN useradd web

RUN pip3 install -r requirements.txt
RUN pip3 install gunicorn

# move database for backup
RUN mkdir /data; chown -R web.web /data /app
VOLUME ["/data", "/secret"]
RUN setuser web ln -s /data/db.sqlite3 db.sqlite3

ADD conf/service /etc/service/
ENV DJANGO_SETTINGS_MODULE=gmailpurge.settings_prod

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*