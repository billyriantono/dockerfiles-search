FROm debian:jessie

MAINTAINER Bill Lee "bill.lee.y@gmail.com"

RUN apt-get update && \
    apt-get install -y uwsgi \
        uwsgi-plugin-python \
        python-pip \
        python-dev && \
    apt-get clean

COPY uwsgi.ini /etc/uwsgi/uwsgi.ini
RUN useradd -r -s /bin/false -U uwsgi

EXPOSE 3031
