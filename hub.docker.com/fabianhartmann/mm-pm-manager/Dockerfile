FROM ubuntu:14.04
MAINTAINER fabian.hartmann@bluewin.ch

# Enviroment Variables for Datacontainer and Restore from Backup.
ENV AUTODISABLEDEPRECATED=true
ENV AUTOSECURITYUPDATES=true
ENV PURGEDEPRECATED=true
ENV AUTOUPDATEPATTERNS="XProtect\|Core Suggestions Configuration Data\|MRT Configuration Data\|Gatekeeper Configuration Data\|Incompatible Kernel Extension Configuration Data\|System Integrity Protection Configuration Data\|Security Update"

# Installs nessesary binarys.
RUN \
	sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  # echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list && \
	apt-get update && \
	apt-get -y upgrade && \
	apt-get -y install git python-setuptools python curl python-pip cron screen supervisor && \
	rm -rf /var/lib/apt/lists/* && \
	easy_install flask && \
	easy_install simplejson

# installs reposado and margarita
RUN mkdir /usr/local/asus && \
	cd /usr/local/asus && \
	git clone https://github.com/wdas/reposado.git

# adds all the nessesary configuration Files.
ADD CONF/preferences.plist /usr/local/asus/reposado/code/
ADD enablesecurityupdates.sh /usr/local/asus/reposado/code/
ADD removedeprecatedproducts.sh /usr/local/asus/reposado/code/
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# adds my scrippt with some functions.
ADD ./worker.sh /srv/

# adds cron jobs for backup and sync
ADD cron_repo_sync /etc/cron.daily/repo_sync

ENV HOME /root
WORKDIR /srv/MMServiceData/MM-REPOSADO

VOLUME ["/srv/MMServiceData/MM-REPOSADO"]

CMD /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf
