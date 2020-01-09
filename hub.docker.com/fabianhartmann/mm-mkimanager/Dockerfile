FROM ubuntu:14.04
MAINTAINER fabian.hartmann@bluewin.ch

RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get -y install \
  cron \
  supervisor && \
  rm -rf /var/lib/apt/lists/*

RUN mkdir -p /srv/MMServiceData/MM-BACKUP/{CERT,CONF,LOG,REPORT,SCRIPTS,BACKUPS,DATA}

COPY ./cronbackup /etc/cron.hourly/
RUN chmod +x /etc/cron.hourly/*


COPY ./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

COPY ./worker.sh /srv/MMServiceData/MM-BACKUP/SCRIPTS/worker.sh


VOLUME ["/srv/MMServiceData/MM-BACKUP"]

ENV HOME /root

WORKDIR /srv/MMServiceData/MM-BACKUP

CMD /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf
