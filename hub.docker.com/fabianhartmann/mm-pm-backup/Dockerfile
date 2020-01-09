FROM ubuntu:14.04
MAINTAINER fabian.hartmann@bluewin.ch

# Enviroment Variables for Datacontainer and Restore from Backup.

# Installs nessesary binarys.
RUN \
	sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  # echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list && \
	apt-get update && \
	apt-get -y upgrade && \
	apt-get -y install libapache2-mod-wsgi git python-setuptools python curl python-pip cron nano screen supervisor && \
	rm -rf /var/lib/apt/lists/* && \
	easy_install flask && \
	easy_install simplejson

# adds all the nessesary configuration Files.
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# adds my scrippt with some functions.
ADD ./backup.sh /srv/

# adds cron jobs for backup and sync
ADD cron_backup /etc/cron.daily/cron_backup

ENV HOME /root
WORKDIR /srv/MMServiceData/MM-REPOSADO

VOLUME ["/srv/MMServiceData/MM-REPOSADO"]

CMD /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf
