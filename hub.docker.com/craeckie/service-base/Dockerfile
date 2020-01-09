FROM phusion/baseimage:0.9.17

MAINTAINER Josia <josia-login@rosskopfs.de>

ENV Hostname weiltoast.de

RUN echo "Acquire::http::Proxy \"http://$Hostname:3142\";" | tee /etc/apt/apt.conf.d/01proxy

RUN apt-get update
RUN apt-get upgrade -y && apt-get -y dist-upgrade && apt-get install -y nano git build-essential

RUN mkdir -p /etc/my_init.d/

ENV TZ 'Europe/Berlin'

WORKDIR /root

# Configure all cron-jobs by adding all ENV-variables
ADD init-cron.sh /etc/my_init.d/10-init-cron.sh
RUN chmod +x /etc/my_init.d/10-init-cron.sh

ADD util.sh util.sh
RUN chmod +x util.sh
