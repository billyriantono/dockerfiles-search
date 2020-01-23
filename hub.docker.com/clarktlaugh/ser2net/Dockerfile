FROM ubuntu
MAINTAINER Clark Laughlin clark@laughlins.org

RUN apt-get update
RUN apt-get install -y ser2net supervisor

RUN mkdir -p /var/log/supervisor

ADD ser2net.conf /etc/ser2net.conf
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 20115
EXPOSE 20096

CMD ["/usr/bin/supervisord"]
