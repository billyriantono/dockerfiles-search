FROM php:7.0.6-apache
MAINTAINER Hugo Meyronneinc <hugomeyronneinc@gmail.com>


RUN apt-get update
RUN apt-get install -y build-essential libgd2-xpm-dev apache2-utils unzip wget libssl-dev

RUN useradd -m nagios
RUN groupadd nagcmd
RUN usermod -aG nagcmd nagios
RUN usermod -aG nagcmd www-data

WORKDIR /home/nagios

RUN wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.1.1.tar.gz
RUN wget http://www.nagios-plugins.org/download/nagios-plugins-2.1.1.tar.gz
RUN wget http://sourceforge.net/projects/nagios/files/nrpe-2.x/nrpe-2.15/nrpe-2.15.tar.gz

RUN tar zvfx nagios-4.1.1.tar.gz
RUN tar zvfx nagios-plugins-2.1.1.tar.gz
RUN tar zvfx nrpe-2.15.tar.gz

#Nagios install
WORKDIR /home/nagios/nagios-4.1.1
RUN ./configure --with-command-group=nagcmd
RUN make all install install-init install-config install-commandmode
ADD httpd.conf /etc/apache2/sites-enabled/nagios.conf

#Nagios plugins install
WORKDIR /home/nagios/nagios-plugins-2.1.1
RUN ./configure --with-nagios-user=nagios --with-nagios-group=nagios
RUN make install

#NRPE install
WORKDIR /home/nagios/nrpe-2.15
RUN ./configure --with-ssl=/usr/bin/openssl --with-ssl-lib=/usr/lib/x86_64-linux-gnu
RUN make all install install-daemon

#Apache2 configure
RUN a2enmod rewrite
RUN a2enmod cgi

#Nagios config
RUN mkdir /usr/local/nagios/etc/servers/
RUN mkdir /usr/local/nagios/etc/printers/
RUN mkdir /usr/local/nagios/etc/switches/
RUN mkdir /usr/local/nagios/etc/routers/

ADD nagios.cfg /usr/local/nagios/etc/nagios.cfg
ADD cgi.cfg /usr/local/nagios/etc/cgi.cfg

VOLUME /usr/local/nagios/
EXPOSE 80

#Run !
ADD start.sh /home/nagios/start.sh
CMD /home/nagios/start.sh
