FROM debian:latest
MAINTAINER Francesco Sullo, sullof@sullof.com, http://sullof.com , modified by Akos Kovacs

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install python-pip python-dev build-essential 
RUN pip install supervisor
RUN apt-get -y install perl && apt-get -y install perl-doc
RUN apt-get install -y openssh-server python-setuptools && /usr/bin/easy_install supervisor

RUN useradd -d / -g users -p $(perl -e'print crypt("foo", "aa")') -M -N foo

ADD adds/authorized_keys /authorized_keys
ADD adds/configure.sh /configure.sh
RUN bin/bash /configure.sh && rm /configure.sh

ADD adds/supervisord.conf /etc/supervisord.conf

EXPOSE 22

CMD ["/usr/local/bin/supervisord","-n"]

