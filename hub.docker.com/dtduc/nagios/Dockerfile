FROM php:7.3-apache

MAINTAINER dtd<dtduc.contact@gmail.com>

ARG NAGIOS_USER=nagiosadmin
ARG NAGIOS_PASSWORD=nagiosadmin
ARG NAGIOS_VERS=nagios-4.4.3
ARG NAGIOS_PLUGIN_VERS=nagios-plugins-2.2.1
ARG MK_LIVESTATUS_VERS=mk-livestatus-1.2.4p4

ENV E_NAGIOS_USER			$NAGIOS_USER
ENV E_NAGIOS_PASSWORD		$NAGIOS_PASSWORD
ENV E_NAGIOS_VERS 			$NAGIOS_VERS
ENV E_NAGIOS_PLUGIN_VERS	$NAGIOS_PLUGIN_VERS
ENV E_MK_LIVESTATUS_VERS	$MK_LIVESTATUS_VERS
ENV NAGIOS_HOME             /usr/local/nagios
ENV NRDP_TOKEN              culaio239ncgklak
ENV NCPA_TOKEN              mfasjlk1asjd7flj3ly
ENV NAGIOS_GROUP            nagcmd
ENV MYSQL_USER              nagios
ENV MYSQL_PASSWORD          nagios
ENV MYSQL_ADDRESS           mysql
ENV MYSQL_DATABASE          nagios
ENV APACHE_LOCK_DIR /var/run
ENV APACHE_LOG_DIR /var/log/apache2

RUN DEBIAN_FRONTEND=noninteractive

## Prepare packages
RUN apt-get update && apt-get install -y libxml2-dev \
	libpng-dev \
	libgd-dev \
	libperl-dev \ 
	unzip \
	wget \
	libnet-snmp-perl \
	snmp \
	snmpd \
	smistrip \
	vim \
	rsync \
	sqlite \
	graphviz \
    && docker-php-ext-install gd soap gettext sockets

## Create user and group for nagios & ajust apache2 config
RUN useradd nagios && groupadd nagcmd && usermod -a -G nagcmd nagios && usermod -a -G nagcmd www-data \
	&& echo "ServerName localhost" >> /etc/apache2/apache2.conf

## Install snmp-mib-downloader and add confige
RUN cd /tmp \
	&& wget http://ftp.br.debian.org/debian/pool/non-free/s/snmp-mibs-downloader/snmp-mibs-downloader_1.1+nmu1_all.deb \
	&& dpkg -i snmp-mibs-downloader_1.1+nmu1_all.deb \
	&& download-mibs && echo "mibs +ALL" >> /etc/snmp/snmp.conf \
	&& echo "mibdirs +/usr/share/snmp/mibs" >> /etc/snmp/snmp.conf

## Install Nagios
RUN cd /tmp \
	&& wget https://github.com/NagiosEnterprises/nagioscore/releases/download/${E_NAGIOS_VERS}/${E_NAGIOS_VERS}.tar.gz \
	&& tar -zxvf /tmp/${E_NAGIOS_VERS}.tar.gz \
	&& cd /tmp/${E_NAGIOS_VERS}/ \
	&& ./configure --with-nagios-group=nagios --with-command-group=nagcmd \
	&& make all \
	&& make install \
	&& make install-init \
	&& make install-daemoninit \
	&& make install-config \
	&& make install-commandmode \
	&& make install-exfoliation \
	&& cp -R contrib/eventhandlers/ /usr/local/nagios/libexec/ \
	&& chown -R nagios:nagios /usr/local/nagios/libexec/eventhandlers

## Apache2 Configuration
COPY nagios.conf /etc/apache2/conf-available/.

RUN htpasswd -b -c /usr/local/nagios/etc/htpasswd.users $E_NAGIOS_USER $E_NAGIOS_PASSWORD \
	&& a2enconf nagios \ 
	&& a2enmod cgi rewrite \
	&& service apache2 restart

## Install Nagios Plugins
RUN cd /tmp \
	&& wget http://www.nagios-plugins.org/download/${E_NAGIOS_PLUGIN_VERS}.tar.gz \
	&& tar xzf ${E_NAGIOS_PLUGIN_VERS}.tar.gz \
	&& cd $E_NAGIOS_PLUGIN_VERS \
	&& ./configure --with-nagios-user=nagios --with-nagios-group=nagios \
	&& make \
	&& make install 

## Install Nagios MK_LIVE
RUN cd /tmp \
	&& wget http://mathias-kettner.de/download/${E_MK_LIVESTATUS_VERS}.tar.gz \
	&& tar -xzvf ${E_MK_LIVESTATUS_VERS}.tar.gz \
	&& cd $E_MK_LIVESTATUS_VERS \
	&& ./configure CPPFLAGS=-I/Nagios-Sources/${E_NAGIOS_VERS}/include/ --with-nagios4 --prefix=/usr/local/nagios \
	&& make \
	&& make install \
	&& echo "broker_module=/usr/local/nagios/lib/mk-livestatus/livestatus.o /usr/local/nagios/var/rw/live" >> /usr/local/nagios/etc/nagios.cfg \
	&& echo "event_broker_options=-1" >> /usr/local/nagios/etc/nagios.cfg 

## Verify Nagios
RUN /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

## Prepare for Nagvis
RUN cd /tmp \
	&& wget http://www.nagvis.org/share/nagvis-1.9.10.tar.gz \
	&& tar xzvf nagvis-1.9.10.tar.gz 

COPY trigger.sh /tmp/nagvis-1.9.10

RUN cd /tmp/nagvis-1.9.10 \
	&& chmod +x trigger.sh \
	&& ./trigger.sh \
	&& a2enconf nagvis

WORKDIR /usr/local/nagios

COPY start.sh /tmp

RUN chmod +x /tmp/start.sh

EXPOSE 80

ENTRYPOINT ["/tmp/start.sh"]

CMD [ "main" ]
