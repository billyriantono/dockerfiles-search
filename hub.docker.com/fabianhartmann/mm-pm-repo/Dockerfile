FROM ubuntu:14.04
MAINTAINER fabian.hartmann@bluewin.ch

# Enviroment Variables for Datacontainer and Restore from Backup.
ENV VIRTUAL_HOST=asus.example.com
ENV REPOSADOURL=asus.example.com
ENV MARGARITAURL=masus.example.com

# Installs nessesary binarys.
RUN \
	sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  # echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list && \
	apt-get update && \
	apt-get -y upgrade && \
	apt-get -y install libapache2-mod-wsgi git python-setuptools python curl python-pip apache2 screen supervisor && \
	rm -rf /var/lib/apt/lists/*

# enables apaches rewrite module
RUN a2enmod rewrite

ADD ports.conf /etc/apache2/ports.conf
ADD reposado.conf /etc/apache2/sites-enabled/reposado.conf
RUN rm /etc/apache2/sites-enabled/000-default.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf


ENV HOME /root
EXPOSE 80
WORKDIR /srv/MMServiceData/MM-REPOSADO

VOLUME ["/srv/MMServiceData/MM-REPOSADO"]

CMD /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf
