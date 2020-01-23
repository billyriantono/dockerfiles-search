FROM debian:latest

MAINTAINER Frank Fuhrmann <frank.fuhrmann@mailbox.org>

RUN apt-get update && apt-get -y dist-upgrade
RUN apt-get -y install beanstalkd
RUN mkdir -p /var/beanstalkd
RUN chown beanstalkd:beanstalkd /var/beanstalkd
VOLUME /var/beanstalkd
EXPOSE 11300
CMD sh -c '/usr/bin/beanstalkd -l 0.0.0.0 -p 11300 -b /var/beanstalkd -s 209715200'
