# Version 11/2017 

FROM debian:jessie
MAINTAINER Alin Sennewald <alinbuiac@gmail.com>
ENV DEBIAN_FRONTEND noninteractive

# install untils 
RUN apt-get update && apt-get upgrade -y --force-yes && apt-get install -y --force-yes --no-install-recommends apt-utils
RUN apt-get -y --force-yes install wget apt-transport-https
RUN apt-get -y --force-yes install \

unzip \
perl \
git \
apt-transport-https \
sudo etherwake \
dfu-programmer \
build-essential \
snmpd \
snmp \
vim \
telnet \
usbutils \
sqlite3 \

&& apt-get clean

# perl packages
RUN apt-get -y --force-yes install perl-base \
libdevice-serialport-perl \ 
libxml-simple-perl \
libwww-perl \
libio-socket-ssl-perl \ 
libcgi-pm-perl \
libjson-perl \
sqlite3 \
libdbd-sqlite3-perl \ 
libtext-diff-perl \
libtimedate-perl \

&& apt-get clean

# install mqtt
RUN cpan install Net::MQTT:Simple

# install fhem
RUN wget -qO - https://debian.fhem.de/archive.key | apt-key add -
RUN echo "deb https://debian.fhem.de/nightly/ /" | tee -a /etc/apt/sources.list.d/fhem.list
RUN apt-get update
RUN apt-get -y --force-yes install supervisor fhem telnet
RUN mkdir -p /var/log/supervisor

# Timezone
RUN echo Europe/Berlin > /etc/timezone && dpkg-reconfigure tzdata

# install tablet ui
RUN wget https://github.com/knowthelist/fhem-tablet-ui/archive/master.zip
RUN unzip master.zip && rm master.zip
RUN cp -r ./fhem-tablet-ui-master/www/tablet /opt/fhem/www/
RUN cp /opt/fhem/www/tablet/index-example.html /opt/fhem/www/tablet/index.html

RUN apt-get -y --force-yes install at cron && apt-get clean

# sshd on port 2222 and allow root login / password = 
RUN apt-get -y --force-yes install openssh-server && apt-get clean
RUN sed -i 's/Port 22/Port 2222/g' /etc/ssh/sshd_config
RUN sed -i 's/PermitRootLogin no/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN echo "root:0410Jana" | chpasswd
RUN /bin/rm  /etc/ssh/ssh_host_*
RUN dpkg-reconfigure openssh-server

RUN apt-get clean && apt-get autoremove

ENV RUNVAR fhem
WORKDIR /root

# pulsway
RUN wget https://www.pulseway.com/download/pulseway_x64.deb
RUN dpkg -i pulseway_x64.deb && rm pulseway_x64.deb

COPY config.xml /etc/pulseway/config.xml
COPY fhem.cfg /opt/fhem/fhem.cfg
COPY controls.txt /opt/fhem/FHEM/controls.txt

ADD run.sh /root/run.sh
RUN chmod +x /root/run.sh
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ENTRYPOINT ["./run.sh"]

VOLUME ["/opt/fhem"]

EXPOSE 2222 8083 8084 8085
