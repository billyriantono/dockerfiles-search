FROM debian:jessie
MAINTAINER Justus

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y software-properties-common
RUN apt-add-repository non-free
RUN apt-add-repository contrib
RUN apt-get update && apt-get upgrade -y

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get install -y build-essential cmake libperl-dev libssh2-1-dev libgcrypt11-dev libcgsi-gsoap-dev zlib1g-dev libssl-dev libxerces-c-dev librrd-dev libqt4-dev libqt4-sql-mysql lsb-release libgnutls28-dev sudo make curl ncftp bsd-mailx rrdtool librrds-perl libconfig-inifiles-perl libcrypt-des-perl libdigest-hmac-perl  libgd-gd2-perl snmp snmpd libnet-snmp-perl libsnmp-perl fping smbclient postfix snmp-mibs-downloader gawk lynx sqsh grep expect python-pywbem mysql-client htop python-pymssql locate telnet bc nagios-plugins-basic liblwp-useragent-determined-perl libsys-statistics-linux-perl libcache-cache-perl python-pip python-dev libxslt1-dev libxml2-dev python-lxml php5 python-mysql.connector freetds-dev freetds-bin


RUN mkdir downloads && \
	cd downloads/ && \
	wget https://s3-eu-west-1.amazonaws.com/centreon-download/public/centreon-clib/centreon-clib-1.4.2.tar.gz && \
	wget https://s3-eu-west-1.amazonaws.com/centreon-download/public/centreon-connectors/centreon-connector-1.1.2.tar.gz && \
	wget https://s3-eu-west-1.amazonaws.com/centreon-download/public/centreon-engine/centreon-engine-1.5.1.tar.gz && \
	wget https://s3-eu-west-1.amazonaws.com/centreon-download/public/centreon-broker/centreon-broker-2.11.5.tar.gz && \
	tar xzf centreon-clib-1.4.2.tar.gz && \
	tar xzf centreon-connector-1.1.2.tar.gz && \
	tar xzf centreon-engine-1.5.1.tar.gz && \
	tar xzf centreon-broker-2.11.5.tar.gz

## Centreon CLIB
RUN cd /downloads/centreon-clib-1.4.2/build/  && \
	cmake \
	 -DWITH_TESTING=0 \
	 -DWITH_PREFIX=/usr \
	 -DWITH_SHARED_LIB=1 \
	 -DWITH_STATIC_LIB=0 \
	 -DWITH_PKGCONFIG_DIR=/usr/lib/pkgconfig .  && \
	make && \
	make install

##Centreon Connector
RUN cd /downloads/centreon-connector-1.1.2/perl/build  && \
	cmake \
	 -DWITH_PREFIX=/usr \
	 -DWITH_PREFIX_BINARY=/usr/lib/centreon-connector \
	 -DWITH_CENTREON_CLIB_INCLUDE_DIR=/usr/include \
	 -DWITH_TESTING=0 .  && \
	make && \
	make install

RUN cd /downloads/centreon-connector-1.1.2/ssh/build && \
	cmake \
	 -DWITH_PREFIX=/usr \
	 -DWITH_PREFIX_BINARY=/usr/lib/centreon-connector \
	 -DWITH_CENTREON_CLIB_INCLUDE_DIR=/usr/include \
	 -DWITH_TESTING=0 .  && \
	make && \
	make install

##Centreon Engine

RUN groupadd -g 6001 centreon-engine
RUN useradd -u 6001 -g centreon-engine -m -r -d /var/lib/centreon-engine -c "Centreon-engine Admin" centreon-engine

RUN cd /downloads/centreon-engine-1.5.1/build/ && \
	cmake \
	 -DWITH_CENTREON_CLIB_INCLUDE_DIR=/usr/include \
	 -DWITH_CENTREON_CLIB_LIBRARY_DIR=/usr/lib \
	 -DWITH_PREFIX=/usr \
	 -DWITH_PREFIX_BIN=/usr/sbin \
	 -DWITH_PREFIX_CONF=/etc/centreon-engine \
	 -DWITH_USER=centreon-engine \
	 -DWITH_GROUP=centreon-engine \
	 -DWITH_LOGROTATE_SCRIPT=1 \
	 -DWITH_VAR_DIR=/var/log/centreon-engine \
	 -DWITH_RW_DIR=/var/lib/centreon-engine/rw \
	 -DWITH_STARTUP_DIR=/etc/init.d \
	 -DWITH_PKGCONFIG_SCRIPT=1 \
	 -DWITH_PKGCONFIG_DIR=/usr/lib/pkgconfig \
	 -DWITH_TESTING=0 \
	 -DWITH_WEBSERVICE=1 . && \

	make && \
	make install && \
	update-rc.d centengine defaults

##Centreon Broker

RUN groupadd -g 6002 centreon-broker
RUN useradd -u 6002 -g centreon-broker -m -r -d /var/lib/centreon-broker -c "Centreon-broker Admin" centreon-broker
RUN usermod -a -G centreon-broker centreon-engine

RUN cd /downloads/centreon-broker-2.11.5/build/ && \
	cmake \
	 -DWITH_DAEMONS='central-broker;central-rrd' \
	 -DWITH_GROUP=centreon-broker \
	 -DWITH_PREFIX=/usr \
	 -DWITH_PREFIX_BIN=/usr/sbin \
	 -DWITH_PREFIX_CONF=/etc/centreon-broker \
	 -DWITH_PREFIX_LIB=/usr/lib/centreon-broker \
	 -DWITH_PREFIX_MODULES=/usr/local/centreon/lib/centreon-broker \
	 -DWITH_STARTUP_DIR=/etc/init.d \
	 -DWITH_STARTUP_SCRIPT=auto \
	 -DWITH_TESTING=0 \
	 -DWITH_USER=centreon-broker . && \

	make && \
	make install && \
	update-rc.d cbd defaults 
	
## sonstiges

RUN mkdir /var/log/centreon-broker && \
chmod -R 774 /var/log/centreon-broker && \
chmod -R 774 /var/log/centreon-engine && \
chmod -R 774 /etc/centreon-engine && \
chmod -R 774 /etc/centreon-broker && \
chown centreon-engine:centreon-engine  /var/log/centreon-broker && \
useradd -g centreon-engine -m -r -d /var/lib/centreon centreon && \
chown -R centreon /var/lib/centreon 

## passwd centreon #siehe PSR
## passwd centreon-engine #siehe PSR

# usermod -aG centreon-engine centreon
# chmod -R 775 /var/lib/centreon-broker
# chmod -R 774 /etc/centreon-engine
# usermod -a -G centreon-broker centreon

#Fehler SNMP Abfragen
RUN cd /var/lib/centreon/ && \
mkdir centplugins  && \
chown centreon:centreon-engine centplugins/ && \
chmod 775 centplugins/


###################################
#Downgrade sqsh 

RUN apt-get -y remove sqsh

#RUN cat <<eof >/etc/apt/sources.list.d/squeeze.list
#deb http://archive.debian.org/debian/ squeeze contrib main non-free
#eof

RUN echo " \n\
deb http://archive.debian.org/debian/ squeeze contrib main non-free \n\
" >> /etc/apt/sources.list.d/squeeze.list


#RUN cat <<eof >/etc/apt/apt.conf.d/99squeeze
#APT::Default-Release "jessie";
#eof

RUN echo " \n\
APT::Default-Release "jessie"; \n\
" >> /etc/apt/apt.conf.d/99squeeze

RUN apt-get update && \
apt-cache showpkg sqsh
RUN apt-get install -y --force-yes sqsh=2.1-9

#Neue Nagios/Monitoring Plugins

RUN cd /usr/local/src && \
wget https://www.monitoring-plugins.org/download/monitoring-plugins-2.1.2.tar.gz && \
tar xzf monitoring-plugins-2.1.2.tar.gz && \
cd monitoring-plugins-2.1.2 && \
./configure --prefix=/usr/local/nagios --with-nagios-user=centreon-engine && \
make && \
make install
