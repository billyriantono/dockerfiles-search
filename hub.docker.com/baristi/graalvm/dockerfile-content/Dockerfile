FROM ubuntu:xenial

RUN apt-get update &&  apt-get install -y python  python-pip libevent-dev supervisor && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip

RUN pip install flask flask-cors Pillow uwsgi

RUN useradd -m -s /bin/bash ubuntu

ADD webserver /webserver

ADD  supervisord.conf /supervisord.conf

WORKDIR /opt/apps

ENTRYPOINT ["/usr/bin/supervisord","-c","/supervisord.conf"]
