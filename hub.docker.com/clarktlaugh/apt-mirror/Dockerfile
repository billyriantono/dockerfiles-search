FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y openssh-server lighttpd apt-mirror supervisor python-pip
RUN pip install supervisor-stdout

RUN mkdir -p /srv/apt-mirror
RUN mkdir -p /var/run/sshd
RUN mkdir -p /var/log/supervisor
RUN adduser www-data -G www-data -H -s /bin/false -D

VOLUME /srv/apt-mirror

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD mirror.list /etc/apt/mirror.list
ADD lighttpd.conf /etc/lighttpd/lighttpd.conf

EXPOSE 80
EXPOSE 22

CMD ["/usr/bin/supervisord"]
