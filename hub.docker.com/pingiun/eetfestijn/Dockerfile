FROM python:3

MAINTAINER Jelle Besseling <jelle@pingiun.com>

COPY . /app

WORKDIR /app

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get -y upgrade \
    && DEBIAN_FRONTEND=noninteractive apt-get -y install libffi-dev libxml2-dev libxslt1-dev zlib1g-dev locales

# Set the locale
RUN echo 'nl_NL.UTF-8 UTF-8' > /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales

RUN pip install uwsgi && pip install -r requirements.txt

VOLUME ["/app/socket/"]

ENV UWSGI_MOUNTPOINT /

ENV UWSGI_APP eetfestijn.wsgi:application

ENV DEBUG False

RUN SECRET_KEY=notneeded /app/manage.py migrate

CMD /usr/local/bin/uwsgi -s /app/socket/uwsgi.sock --http :9000 --manage-script-name --mount $UWSGI_MOUNTPOINT=$UWSGI_APP
