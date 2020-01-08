FROM debian:jessie
MAINTAINER Andrew Smith "andrew1972.es@gmail.com"

ADD sources.list /tmp/sources.list
RUN cat /tmp/sources.list > /etc/apt/sources.list 
RUN rm -f /tmp/sources.list

RUN apt-get update
RUN apt-get -y install supervisor net-tools

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD run.sh /run.sh
RUN chmod +x /run.sh

CMD ["/run.sh"]
