# MongoDB 
#
# VERSION               0.0.1

FROM      ubuntu
MAINTAINER Jeffery Utter "jeff@jeffutter.com"

ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get -y install memcached 

EXPOSE 11211 

CMD  ["memcached", "-u", "daemon"]
