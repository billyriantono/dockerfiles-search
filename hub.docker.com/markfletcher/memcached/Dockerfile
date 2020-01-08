FROM ubuntu:trusty
MAINTAINER Mark Fletcher

#install memcached
RUN echo 29-07-2014
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y memcached pwgen

ADD run.sh /run.sh
RUN chmod 755 /run.sh

EXPOSE 11211

CMD ["/run.sh"]
