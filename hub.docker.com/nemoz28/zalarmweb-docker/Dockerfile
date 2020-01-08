FROM debian:jessie

MAINTAINER Jerome Zamaroczy

ARG HOST="localhost"
ENV HOST=${HOST}

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN (apt-get update && \
     apt-get upgrade -f -qq -y && \
     apt-get install -y python3-pip python3-django redis-server git python3-flask python3-serial curl vim net-tools htop   && \
     pip3 install Django==1.8.1 django-bootstrap3 django-redis django-bootstrap-static django-bootstrap-themes \
     django-debug-toolbar django-extensions django-redis-cache django-redis-views django-websocket-redis hiredis  \
     git+https://github.com/dpallot/simple-websocket-server.git \
     daemonize psutil glob2 simplejson  && \
     apt-get clean)

RUN easy_install3 -U pip && \
    pip3 install --upgrade slackclient

COPY etc/init.d/start.sh /etc/init.d/start.sh
COPY etc/redis/data-dev-zalarm.py /etc/redis/data-dev-zalarm.py
RUN chmod +x /etc/init.d/start.sh


VOLUME ["/var/lib/ZalarmWeb"]
VOLUME ["/var/lib/ZalarmPi"]
WORKDIR /var/lib/

RUN mkdir /var/log/zalarm/
RUN touch /var/log/zalarm/zalarmpi.log
RUN echo "***ZalarmDevContener***" > /etc/motd
RUN chmod 774 /var/log/zalarm/zalarmpi.log


EXPOSE 9001 5000 8000

CMD ["/bin/bash", "/etc/init.d/start.sh", "-d"]
