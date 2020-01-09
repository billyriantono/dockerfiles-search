FROM phusion/baseimage
RUN apt-get -y update && apt-get -y install python-pip && pip install supervisor
VOLUME /app
WORKDIR /app
CMD ["/usr/local/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]
