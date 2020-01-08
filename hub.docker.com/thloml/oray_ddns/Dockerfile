FROM ubuntu:16.04

ENV ORAY_HOME /data
RUN mkdir -p ${ORAY_HOME}

RUN mkdir -p /tmp/
add phddns_3.0_x86_64.deb /tmp/pddns.deb
RUN dpkg -i /tmp/pddns.deb && rm /tmp/pddns.deb


RUN apt-get update && apt-get install -y supervisor
ADD supervisord.conf /supervisord.conf
COPY /supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 6060

CMD ["/usr/bin/supervisord"]
